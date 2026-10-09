# What kind of network is the cap? ResNet, transformer, CNN, or something else

Prepared for charlie by Capstan, 2026-10-09. Read from the code that ran: `src/pccap/revision_v1/reader.py`,
`controller.py`, `observations.py`, `memory.py`, `learner.py` (the learned reader, v1/v5) and `src/pccap/cap/`
(stable v0). Parameter counts are computed from the layer shapes in `init_reader` and `init_controller` and agree with
the 3,348,228 that Capex counted from the saved arrays.

## 1. The short answer

The cap is none of the three named families. It is a **memory-augmented retrieval module**: a small feed-forward
encoder, a content-addressed external memory of records, a softmax read-out over the nearest records with an explicit
"none of these" option, and an **additive intervention** on the residual stream of a frozen transformer. The closest
textbook labels are *memory network* (or *key-value memory*, *nearest-neighbour memory*), *single-head attention over
an external memory*, and *activation steering*. The only convolution-free, recurrence-free, attention-free parts are
plain multilayer perceptrons.

Three clarifications that usually resolve the confusion:

- **The transformer is the base, not the cap.** GPT-2 is a transformer; it is frozen; the cap reads from it and adds to
  it. The cap contains no attention over tokens, no positional encodings and no transformer blocks of its own.
- **The residual connection belongs to GPT-2, not the cap.** A transformer *is* a residual network in the ResNet sense
  (every block adds to a running vector). The cap's writes are additions onto that same running vector, so the cap is
  best described as an extra, externally controlled residual branch bolted onto a residual network. Internally the cap
  has no skip connections at all.
- **Stable v0 is not a neural network.** It has no trained weights. It is a nearest-neighbour lookup table with
  calibrated radii whose stored values were taught by gradient steps.

## 2. The labels, so the comparison is fair

| Family | Defining feature | Present in the cap? |
| --- | --- | --- |
| Convolutional network (CNN) | weight sharing across spatial or temporal shifts; local receptive fields | no |
| Residual network (ResNet) | each layer adds its output to its input (skip connections) | not inside the cap; the cap *writes into* GPT-2's residual stream |
| Transformer | self-attention over a sequence of tokens plus per-token MLPs, stacked | no; the cap never looks at tokens as a sequence, only at summary vectors the transformer already computed |
| Multilayer perceptron (MLP) | dense layers with a nonlinearity between | yes: every learned piece of the cap is an MLP of one to three dense layers with GELU |
| Memory network / key-value memory | an external store of (key, value) pairs addressed by similarity to a query | yes: this is the cap's central structure |
| Attention (single head, external) | softmax over query-key similarities, weighted sum of values | yes, in the read-out: a softmax over the top-4 record scores plus one learned null logit |
| Nearest-neighbour / kernel method | prediction by comparing to stored examples rather than by learned weights | yes: records are stored examples; v0 is pure nearest-neighbour |
| Activation steering / additive intervention | add a vector to an internal activation of a frozen model | yes: the write |
| Adapter / LoRA / weight editing (ROME, MEMIT) | change or augment the base's weights | no: no base weight or base-side matrix is ever modified |

## 3. The learned cap (v1, selected configuration v5), piece by piece

Data flow for one query, from the prompt to the modified next-token distribution:

```text
prompt tokens
   │
   ▼
frozen GPT-2 (clean pass, no writes)                 ← transformer, 124M, untouched
   │  read at three taps (after blocks 4, 8, 12):
   │  per tap: the 768-vector at the last position, and the mean 768-vector over the prompt span
   ▼
[1] tap encoder: per tap, LayerNorm each, concatenate (1,536) → dense → 256; sum over taps; GELU
   │                                                   ← three parallel linear layers; MLP-style
   ▼
[2] query head: 256 → 256 → 256 (GELU between)        ← two-layer MLP; the same head produced every stored key ("siamese")
   │
   ▼
[3] retrieval: cosine similarity of the query against every active record key; keep the top 4
   │                                                   ← nearest-neighbour search over an external memory
   ▼
[4] applicability: softmax over [4 scaled cosine scores + lexical-overlap bonus, null logit]
   │   null logit = linear(query) + MLP([q, k_best, q·k_best]: 768 → 256 → 1) − lexical term
   │                                                   ← one attention head over memory with a learned "no key" option
   │   null mass ≥ 0.5  →  stop; return the clean pass unchanged (zero write, exact)
   ▼
[5] payload: the selected record's stored write vectors for this answer position (3 × 768)
   │   scaled by the non-null mass, then rescaled if Σ‖w_m‖/b_m > 0.3
   │                                                   ← table lookup; no network
   ▼
[6] write: add the three vectors to the residual stream at the last position after blocks 4, 8, 12;
   │   resume GPT-2 from the saved block-4 state                 ← additive intervention on a frozen model
   ▼
next-token distribution
```

Two further MLPs exist but are not on the main inference path of the selected configuration:

- **Code head** (256 → 256 → 256): turns an observation of a prompt plus answer into a 256-number "fact code" when a
  record is created.
- **Controller** (512 → 512 → 512 → 2,304, reshaped to 3 × 768): generates writes from [query; fact code]. In v5 the
  taught per-position delta *replaces* the controller's output whenever the record has one, which every taught record
  does, so at query time the controller is bypassed. It served records without deltas in earlier configurations.

### Parameter accounting (slow weights, trained once by backprop, then frozen)

| Component | Shape | Parameters |
| --- | --- | ---: |
| Tap encoder, three taps | 3 × (1,536 → 256) | 1,180,416 |
| Query/key head (tied) | 256 → 256 → 256 | 131,584 |
| Code head | 256 → 256 → 256 | 131,584 |
| Null: query-only term | 256 → 1 | 257 |
| Null: pairwise term | 768 → 256 → 1 | 197,121 |
| Lexical weights | two scalars | 2 |
| **Reader total** | | **1,640,964** |
| Controller | 512 → 512 → 512 → 2,304 | 1,707,264 |
| **Total** | | **3,348,228** |

Every one of these is a dense layer; the only nonlinearity is GELU, the only normalisation is a parameter-free
LayerNorm on the tap inputs and L2 normalisation before the cosine. There is nothing convolutional, nothing recurrent,
and no attention over token positions.

### State accounting (fast state, grows with every taught fact)

The memory is a list of records. Each record holds a 256-number key, a 256-number code, the prompt's token ids, and
the taught delta: 3 × 768 numbers per answer token. Records are append-only; a revision supersedes an older record
rather than overwriting it. Retrieval is deterministic. A 64 MiB ceiling is enforced on every insertion. This store is
where the "learning" of a fact lives; the 3.35M reader weights never change during a stream.

## 4. Stable v0: a lookup table with calibrated radii

The first-month cap has no trained weights at all:

```text
clean residual at site m, last position
   → key = LayerNorm(h) / √768                           (parameter-free)
   → nearest stored key within radius ρ_m, if any       (radius calibrated once on development data)
   → add that slot's stored 768-vector at site m
   → continue to the next block; repeat at sites 2 and 3 in the same pass
```

Three independent banks, one per site, each a fixed-capacity array of (key, value) slots. The values were taught by
normalised gradient steps (adjoint or error-inference credit) under the same write budget. In machine-learning terms
this is a **non-parametric nearest-neighbour memory** with a hard radius gate; the only numbers fitted are the three
radii and the three residual scales b_m. Its known weakness, that a radius cannot tell a paraphrase of a stored fact
from a prompt about a neighbouring fact, is exactly the weakness of a fixed-metric nearest-neighbour rule, and the
learned reader exists to replace that fixed metric with a learned one.

## 5. The random reader

Same architecture as the learned reader, same gate, same memory and same write mechanism, but the 3.35M reader
weights are left at their random initialisation and never trained. It is the control that separates "having a
learned similarity space" from "having a memory and a gate at all". The 44- and 56-point paraphrase-retention gaps on
the "Retrieval is central" slide are the value of training those weights.

## 6. What this architecture is closest to in the literature

| Known system | Shared idea | Difference |
| --- | --- | --- |
| Memory networks; Neural Turing Machine; key-value memory networks | external memory addressed by content similarity, read by softmax | ours writes into a frozen transformer's activations rather than producing an output directly |
| kNN-LM | retrieve stored examples by hidden-state similarity at inference | kNN-LM mixes next-token distributions; ours adds residual vectors and has a learned null |
| Hopfield networks (modern, continuous) and attention | softmax retrieval over stored patterns is one step of a modern Hopfield network and is also one attention head | ours has a top-k cut, an explicit null key and a lexical-overlap feature |
| Activation steering; "function vectors"; ROME-style rank-one edits | change behaviour by adding a vector at a residual site | steering uses one fixed vector; ROME edits weights permanently; ours stores one vector set per fact and gates it |
| Adapters, LoRA | small trainable module beside a frozen base | adapters change every forward pass through learned weights; ours fires only when a record applies and otherwise is an exact no-op |
| Mixture of experts | a gate decides which component acts | our "experts" are stored vectors, and the gate has a null |

## 7. Three kinds of learning, three kinds of state

| What changes | When | By what rule | Paradigm |
| --- | --- | --- | --- |
| Reader and controller weights (3.35M) | once, before any stream; 300 steps on episodes built from development pools | backprop (the PC-trained reader experiment used ePC instead) | ordinary supervised training of a small MLP system |
| Per-fact deltas (3 × 768 per answer token) | during the stream, when a fact is taught | up to five normalised steps along the adjoint, or the error-inference direction, under the write budget | gradient-taught non-parametric memory values |
| v0 radii and site scales | once, on development prefixes | median residual norms; largest radius with ≤ 1 % false fires | calibration, not learning |

The base's weights change under none of these.

## 8. Why "transformer" and "ResNet" are the wrong words even though both are involved

The confusion is natural because the cap is defined entirely in relation to a transformer. It reads the transformer's
residual stream and it writes into the transformer's residual stream. But those are properties of the *interface*, not
of the cap. Inside the interface there is a small MLP encoder, a learned similarity, a memory, a softmax with a null,
and a table of stored vectors. If one had to pick a single name, "a gated key-value memory that steers a frozen
transformer" is accurate, and "a 3.35M-parameter feed-forward reader over an append-only record memory, writing
bounded corrections into GPT-2's residual stream at three depths" is complete.

## Sources

1. `pc_cap/src/pccap/revision_v1/reader.py` (`init_reader`, `embed`, `pair_scores`, `null_score`, `applicability`).
2. `pc_cap/src/pccap/revision_v1/controller.py` (`init_controller`, `bound_writes`, `writes_with_delta`,
   `delta_replaces_controller=True`).
3. `pc_cap/src/pccap/revision_v1/observations.py` (clean-pass taps: last-position and span-mean vectors).
4. `pc_cap/src/pccap/revision_v1/memory.py` and `contracts.py` (`MemoryRecord`, `RecordStore`, 64 MiB ceiling).
5. `pc_cap/src/pccap/revision_v1/learner.py` (`predict`: selection once per query, clean pass then partial corrected pass).
6. `pc_cap/src/pccap/cap/features.py`, `bank.py`, `cap.py`, `calibrate.py` (stable v0).
7. `assets/support-information/gpt2-blocks-cap-layers-and-distillation.md` (Capex, 2026-10-07) for the saved-array
   parameter count.
