# GPT-2, our caps, and distillation: the architecture from first principles

Prepared for charlie by Capex, October 7, 2026. This describes the implementation and saved checkpoints used in this project, including the completed experiment that restricted the cap to upper-layer interfaces. It assumes no prior knowledge of neural-network architecture.

**Our main GPT-2 has 12 transformer blocks. The cap connects to three places in that model: after blocks 4, 8 and 12. Those are three access points, not three additional transformer blocks.** The learned cap contains smaller neural networks plus an editable memory. Stable v0 instead uses a fixed retrieval rule and correction-memory banks.

All 12 GPT-2 blocks still participate in producing predictions. Reading only selected blocks does not remove the others. Likewise, the distillation run copied behavior into a model with the same 12-block architecture; it did not compress GPT-2 into a three-block cap.

**A correction to earlier wording:** `epc-50m` means the ePC checkpoint produced by the approximately **50-million-training-token** run. It is not a 50-million-parameter model. Its saved weights contain **124,439,808 parameters**, the same architectural parameter count as our GPT-2 small. The earlier slide-10 and slide-24 supplements described this ambiguously or incorrectly; their wording has been corrected.

## 1. The objects we need to distinguish

Imagine a machine that receives a piece of text and prepares a prediction of the next piece. To understand its internals, distinguish these terms:

| Term | Meaning here |
| --- | --- |
| Token | A piece of text, such as a word, word fragment or punctuation mark. |
| Weight or parameter | A stored number defining how the machine transforms its input. Learning can change these numbers. |
| Activation | A temporary number produced while processing a particular input. New text produces new activations. |
| Vector | An ordered list of numbers. It is a representation, not necessarily a list of individually interpretable concepts. |
| Layer | A stage of numerical processing. Authors sometimes use this word for a simple operation and sometimes for a larger repeated unit. |
| Transformer block | A larger repeated unit containing attention, a small feedforward network, normalization and addition operations. |
| Cap | Our added retrieval-and-correction machinery, with its own stored information. |

“Frozen” describes the model's **weights**. A frozen model still computes different activations for different inputs. A cap can also change its activations without changing its weights.

An analogy is a fixed recipe applied to changing ingredients. Keeping the recipe fixed does not mean that the intermediate mixtures or final output are always identical. The analogy is limited, but it helps separate permanent settings from temporary computation.

## 2. Which GPT-2, and how many layers?

The model used for the main study is **GPT-2 small**, commonly called GPT-2 124M. In this project's implementation:

| Property | Value | What it counts |
| --- | ---: | --- |
| Transformer blocks | **12** | Successive processing blocks |
| Attention heads per block | **12** | Parallel attention calculations inside each block |
| Residual-stream width | **768** | Numbers representing each token position between blocks |
| Feedforward intermediate width | **3,072** | Numbers temporarily used inside each block's feedforward component |
| Vocabulary size | **50,257** | Possible token identities |
| Maximum position-embedding length | **1,024** | Token positions supported by this GPT-2 configuration |
| Model parameters | **124,439,808** | Stored learned weights and biases, counting the shared input/output embedding once |

“12 layers” in the usual description of this GPT-2 means **12 transformer blocks**, not only 12 matrix operations. A block contains several operations. Token embeddings come before the blocks; final normalization and the output projection come after them. They are not counted as extra transformer blocks.

The 12 attention heads operate in parallel inside a block. They are not another stack of 12 blocks. Each head uses a 64-number attention representation because 768 / 12 = 64.

These counts are for the particular GPT-2 small architecture we used. “GPT-2” names a family, so the name by itself is not a universal layer count. [Sources 1–2.]

## 3. A trip through one transformer prediction

### First, represent the text as numbers

The tokenizer divides the text into tokens and assigns each a vocabulary ID. An **embedding table** turns each ID into a 768-number vector. A position embedding supplies information about where that token occurs.

If the current text has 20 tokens, the model begins with 20 such vectors. Every transformer block processes that collection. The model is not limited to one 768-number vector for the entire sentence.

### Inside each block

Two main transformations occur:

1. **Attention:** each token position can draw information from permitted positions in its context. Twelve heads calculate different learned ways of combining that information. A causal mask prevents a position from seeing later tokens that would not yet be available when generating text.
2. **Feedforward processing:** each position's vector passes through a numerical transformation that expands it from 768 to 3,072 numbers, applies a nonlinear function, and maps it back to 768. This part processes positions individually; attention is the part that directly combines information across positions.

**Layer normalization** regulates the scale of numbers before these transformations. **Residual connections** add each transformation's contribution to the vector already travelling through the model. The running collection of vectors is called the **residual stream**.

A simplified description of one block is:

```text
incoming representation
    → normalize → attention → add to incoming representation
    → normalize → feedforward transformation → add again
    → outgoing representation
```

This repeats for all 12 blocks. Each block has its own learned parameters. “Deeper,” “later” and “upper” refer here to blocks closer to the final output, regardless of whether a diagram draws them upward, downward or sideways.

### Finally, turn the representation into predictions

After block 12, final normalization is followed by an output projection that produces a score for each of the 50,257 vocabulary tokens. Softmax converts those scores into probabilities.

The output projection reuses the token embedding weights. This is called **weight tying**; it avoids treating the input and output embedding tables as two independently learned copies.

For the next-token prediction, we use the output at the final position of the supplied prefix. That position's representation can contain information gathered from earlier tokens through attention.

The model uses all 12 blocks in this prediction. None of the first three blocks is discarded just because our first cap connection is after block 4.

## 4. Exactly where the cap connects

The three standard interfaces are:

| Cap bank or site number | Human block number | Zero-based block index in code | Location |
| --- | ---: | ---: | --- |
| 1 | 4 | 3 | After block 4, before block 5 |
| 2 | 8 | 7 | After block 8, before block 9 |
| 3 | 12 | 11 | After block 12, before final normalization and the vocabulary projection |

The difference between “4” and “3” in the first row is merely a counting convention: people normally start at 1; the code starts at 0.

In this context, **tap**, **site** and **bank** refer to related but slightly different things. A tap is where we observe a representation. A write site is where we can add a correction. A v0 bank is the memory associated with a site. Revision v1 uses a shared record store whose records can supply corrections for all three sites.

At a write site, the basic operation is:

```text
corrected 768-number activation
    = original 768-number activation + 768-number correction
```

The addition happens at the last token position of the current prefix. It does not rewrite GPT-2's stored weights or replace every token's activation in the passage.

The later computation then processes that changed activation. A correction after block 4 can affect the computation in blocks 5–12. A correction after block 8 can affect blocks 9–12. A correction after block 12 goes directly through final normalization and the output projection; there is no block 13.

The three locations therefore have different consequences even though their vectors all contain 768 numbers. [Sources 1 and 3.]

## 5. How a cap can read late information and write earlier

This is a particularly important detail. In the main learned-reader condition, retrieval observations come from a **clean pass through the frozen base with no cap writes**.

That first pass computes the whole model and supplies observations after blocks 4, 8 and 12. The reader uses those observations to decide which stored correction applies, or whether no correction should apply.

When a correction applies, we can reuse the saved clean activation at the earliest write site and recompute the remaining portion with writes:

```text
Clean observation pass:
text → embeddings → blocks 1–4 → blocks 5–8 → blocks 9–12 → base output
                         │             │              │
                         └──────── observations ───────┘
                                         ↓
                                reader + memory selection

Corrected continuation:
saved state after block 4
    → add site-1 correction → blocks 5–8
    → add site-2 correction → blocks 9–12
    → add site-3 correction → final normalization/output
```

Thus information read after block 12 can help select a correction that will be added after block 4 **in the subsequent corrected computation**. This does not make information travel backward in time inside the original forward pass.

Reusing saved computation is also different from ignoring lower layers. Blocks 1–4 already produced the state being reused. When a query is rejected by the cap's null decision, its output is the uncapped base output and no corrective continuation is needed.

For a factual answer, the learned reader selects a record from the prompt and keeps that selection for the answer's successive token positions. Those positions can use different stored correction vectors. In the ordinary-text harm assay, the evaluator instead makes a fresh selection for each scored prefix. The retrieval policy matters when interpreting what the cap reads. [Sources 3–4.]

## 6. How many layers does the learned cap have?

It is a collection of small components, rather than a miniature 12-block transformer. There is no single honest transformer-block count to attach to the whole cap.

The following describes the selected main learned-reader checkpoint. In the table, a **dense layer** means a learned matrix transformation plus a bias: a way to mix an input list of numbers into an output list. A small network with several such stages is often called an **MLP**, short for multilayer perceptron.

### Reading the frozen model's representations

At each of the three taps, the cap extracts:

- the 768-number activation at the prefix's final position;
- a 768-number summary formed by averaging activations over the specified text span.

For initial prompt selection, the span is the prompt. Other code paths use an answer span to initialize a record's answer code, or preserve the prompt span while processing answer prefixes.

At each tap, the two separately normalized vectors are concatenated into **1,536 numbers** and projected into **256 numbers**. The three tap projections have separate learned weights. Their outputs are added together and passed through a nonlinear function.

That sum does not require equal influence from every tap. Each projection can learn a different transformation and scale. What the architecture provides is access to all three; it does not force block 12 to dominate or the earlier taps to contribute equally.

### The small networks and their sizes

| Component | Numerical dimensions | Learned dense stages | Role |
| --- | --- | ---: | --- |
| Each tap projection | 1,536 → 256 | 1 per tap, three parallel branches | Compress that tap's last-position and span features |
| Shared query/key head | 256 → 256 → 256 | 2 | Represent a query and a stored prompt in a comparable space |
| Initial code head | 256 → 256 → 256 | 2 | Produce a compact code from a supplied prompt-and-answer example |
| Pairwise null head | 768 → 256 → 1 | 2 | Help decide whether the best memory candidate should be rejected |
| Query-only null term | 256 → 1 | 1 | Another learned contribution to the rejection score |
| General correction controller | 512 → 512 → 512 → 2,304 | 3 | Convert a query plus code into three 768-number writes |

“Head” here means a small output branch of a network. A reader head is not an attention head in GPT-2.

The query/key head's weights are shared between the two uses. The reader also uses token-overlap features and explicit gating rules. For example, the selected main condition requires a shared sufficiently rare prompt token to avoid applying an edit to a similar question about another subject.

Following the query embedding alone, one travels through a tap projection and then two query-head transformations: **three learned dense stages along that path**. The projections are parallel, not three successive layers. Other branches have different paths, so calling the entire cap “a three-layer network” would conceal much of its structure.

### The parameter count is not the memory capacity

The selected checkpoint contains:

| Reusable component | Saved parameters |
| --- | ---: |
| Reader, including code and null branches | 1,640,964 |
| General correction controller | 1,707,264 |
| Total | **3,348,228** |

That is about **2.69%** of the base model's parameter count. These numbers were counted from the actual saved array shapes, rather than estimated from the name “small cap.”

The acquired correction memory is additional storage. More facts or longer taught answers can require more stored vectors even while the reusable network has the same parameter count. A claim about “3.35 million cap parameters” does not describe all memory usage or all computation. [Sources 5–7.]

## 7. Which of those components supplies the corrections in the main experiment?

The general controller is present in the saved package and participates in the broader training/implementation design. However, **the main v5 deployment uses explicitly acquired correction vectors when a record has them**.

Each such record stores one set of three 768-number corrections per taught answer position. These are called **deltas**. Acquisition optimizes them to increase the probability of the supplied target tokens, using up to five adjoint update steps per answer prefix and an aggregate write-size constraint.

An adjoint is a derivative calculation that tells us how changes to the correction vectors would affect answer loss. It can differentiate through the frozen transformer while leaving every transformer weight fixed.

At query time, the learned reader finds the relevant record. Its stored delta for the current answer position replaces the general controller's code-generated write in this configured path. The implementation retains a controller path for records without a delta. When the selected delta record runs out of taught answer positions, this configuration returns to no write.

This is why the 3.35-million-parameter package should not be pictured as a neural network that freshly synthesizes every main-study correction at every query. Much of the effective answer-specific information lives in the separately acquired delta memory.

It is also why “we trained the reader” and “we taught a new fact” are different events. The reader's reusable weights were frozen for the final edit streams; teaching an edit changed the memory. [Sources 6–8.]

## 8. How stable v0 and the random-reader comparison differ

### Stable v0

Stable v0 has three correction-memory banks at the same block boundaries. In the main stable-v0 condition, a site's 768-number activation is centered and normalized using a fixed mathematical rule to produce its retrieval key.

It compares that key to stored keys and uses a calibrated distance threshold to decide whether to retrieve a correction. Its key transformation is not a trained MLP. The stored value is a 768-number activation correction.

The three banks are memory interfaces, not three transformer blocks. Stable v0 still learns stored correction values during edit acquisition. “No learned reader” does not mean “no learning.”

Stable v0 obtains all its keys from the clean, write-free pass. The older **live-key v0** instead allows earlier writes to change the activations from which later keys are read. Both use the same three possible block boundaries; they differ in which version of the activations supplies retrieval information.

### Random geometry

The main random-reader comparator retains the revision cap's observation and record-memory approach but uses untrained random reader geometry. Its construction disables some learned condition features, including lexical and pairwise-null components, and uses different gate settings. It is therefore not identical to the learned condition with just one switch flipped.

Its read/write sites remain after blocks 4, 8 and 12. A reader can be random or fixed while its answer-specific correction memory still learns.

### Predictive-coding variants

The later PC credit and PC reader experiments alter learning procedures, not the meaning of “12 transformer blocks.” Eight PC settling iterations mean eight iterations of a learning calculation, not an eight-layer cap. A forward-only evaluation can use weights or memories obtained through PC training without running those training iterations on every ordinary prediction. [Sources 8–10.]

## 9. Three different uses of GPT-2 information that can sound like “distillation”

### A. Using frozen activations as features for the cap

In the main experiment, GPT-2 acts as a fixed representation-producing machine. The cap reads selected internal activations and learns how to retrieve and apply corrections using them.

The reader compresses numerical features into smaller embeddings, but it is not trained as an independent language model that replaces GPT-2. It still needs GPT-2 when answering. The supplied factual target also comes from the editing dataset, not from asking the frozen base to invent a new answer. Some targets intentionally differ from what the original model would predict.

Cap training combines answer/retrieval objectives with preservation objectives. On examples that should be left alone, the clean base's predictions provide a reference distribution. That preservation term has a teacher-like role: preserve the base's behavior where an edit should not apply. It is different from distilling the whole language model into the cap.

### B. Actual GPT-2-to-ePC distillation: the REG run

The earlier regeneration run explicitly used a **teacher** and a **student**:

1. The teacher was the frozen pretrained GPT-2 small.
2. The student had the same GPT-2 architecture and initially the same weights.
3. Both processed the training text from the declared OpenWebText shard.
4. The teacher supplied a full next-token probability distribution, giving information about alternatives as well as its favorite token.
5. A predictive-coding training procedure adjusted the student's weights under the distillation objective.
6. The resulting student checkpoint was subsequently frozen when used as a base for the relevant cap experiments.

The teacher probabilities and student probabilities were compared using temperature-scaled KL. Temperature 2 softened the distributions by dividing their scores by 2 before converting them to probabilities; the loss included the associated temperature-squared multiplier. Temperature here is a numerical setting, not physical heat.

There was **no reduction from 12 blocks to three**, or from 124 million parameters to 50 million. The name `epc-50m` refers to the nominal 50,000,000-token training budget. The final saved state records **50,001,920 tokens**, because training finished a complete batch.

The actual teacher target was at the vocabulary-output level. We did not separately require the student's block 4 activation to equal the teacher's block 4 activation, and likewise for every other block. Instead, the PC procedure used internal prediction-error variables across the student's **12 blocks** to obtain local learning signals while responding to the output objective.

The output loss directly reaches the final normalization and shared embedding in that local weight phase; the blocks receive their local error-based terms. This is an asymmetry in how learning signals are formed. It is not a policy of excluding lower blocks from training. [Sources 11–13.]

### C. The separate S1 continuation controls

The project also contains an **S1_literal** self-distillation control: a student starts identical to its frozen teacher and minimizes the same-distribution KL objective. In exact arithmetic the starting discrepancy and gradient are zero. Its measured numerical behavior is a control, not evidence of substantial new knowledge acquisition.

**S1_LM** instead continues language-model training on ordinary text using the actual next tokens as targets. These are separately named control bases, frozen before their cap evaluations. Neither should be confused with teaching the main frozen GPT-2 the final factual-edit targets by changing its own weights. [Source 14.]

## 10. Are lower layers being ignored? The precise answer

There are several different questions hidden in “ignored”:

| Question | Main configuration |
| --- | --- |
| Are some GPT-2 blocks removed from the prediction computation? | **No.** All 12 contribute. |
| Does the cap directly read every block's output? | **No.** It reads after 4, 8 and 12. |
| Does the cap directly write at every block? | **No.** It writes at those three sites. |
| Do lower blocks contribute indirectly to later observed representations? | **Yes.** The later states were computed from their outputs. |
| Does the cap have an upper half of transformer blocks that we preferentially use? | **No.** It has the branched smaller networks and memory described above. |
| Does the main architecture force the latest tap to matter most? | **No.** It has distinct learned tap projections; actual influence is not fixed by the layer numbers alone. |
| Does distillation train only the student's final blocks? | **No.** Its local PC weight-update construction includes all 12 blocks. |

There is a real asymmetry in **intervention depth**. In a corrected pass, the first direct intervention follows block 4. Blocks 1–3 have no direct cap write, and block 4 has already computed its output before that first addition. An early write has more subsequent transformer computation through which to act than a late write.

There is also an asymmetry in **token position**: the write targets the current prefix's final position rather than all positions. Earlier tokens can still influence that position through attention. If a correction changes generated text, the different text can of course affect later predictions, including later computations in lower blocks.

Finally, there is an asymmetry between **observation and intervention**: we observe a clean pass, then intervene in a subsequent computation. Keeping observations clean helps prevent the retrieval query from being altered by the cap's own upstream corrections.

None of these facts establishes that early representations are noise. Their contribution may already be present inside later states even when they are not directly read.

## 11. What happened when we deliberately prioritized upper sites?

The completed **AW-L** experiment directly addressed that possibility. It varied the read and write interfaces independently:

| Condition | Read after blocks | Write after blocks |
| --- | --- | --- |
| Full read, full write | 4, 8, 12 | 4, 8, 12 |
| Upper read, full write | 8, 12 | 4, 8, 12 |
| Full read, last write | 4, 8, 12 | 12 |
| Upper read, last write | 8, 12 | 12 |

“Full” here means all three standard cap sites, not every one of GPT-2's 12 block outputs. In every condition, the underlying transformer still had all 12 blocks.

Upper-only reading removed the block-4 tap projection from the reader. That removed **393,472 reusable parameters**, reducing the saved package from **3,348,228 to 2,954,756**. The remaining head dimensions stayed the same. Last-only writing constrained the correction sites; it did not mean deleting two thirds of GPT-2 or constructing a newly optimized one-output controller from scratch.

The experiment used three paired training seeds and two datasets, giving 24 evaluations across these four configurations. The completed results did not establish the hoped-for advantage:

- Last-only writes increased mean signed ordinary-text loss change in all 12 paired write comparisons, by a factor of **2.64–4.37** relative to the corresponding full-write change.
- The largest absolute change in paraphrase retention from that write restriction was only **0.67 percentage points**.
- Upper-only reading lowered CounterFact paraphrase retention in all three seeds; zsRE effects were mixed.

The ratio concerns the **increment in prediction loss caused by the cap**, not total model error or a multiplier on the number of wrong answers. The [nats guide](nats-from-first-principles.md) and [slide-24 explanation](slide-24-experimental-lessons-and-open-questions.md) explain that distinction.

Readers were trained under the full-write objective, and the write restrictions were tested using separately acquired memories. We did not retrain a specially designed last-only writer. This experiment therefore gives evidence against this restriction as an easy improvement in the tested system; it does not rule out every architecture that emphasizes later layers. [Source 15.]

## 12. A guide to numbers that refer to different things

| Number or name | What it actually means |
| --- | --- |
| GPT-2's 12 layers | 12 transformer blocks |
| 12 attention heads | Parallel attention mechanisms inside each block |
| Banks 1, 2 and 3 | Cap access points after transformer blocks 4, 8 and 12 |
| Reader width 256 | Numbers in a reader representation, not a layer count |
| Top-k 4 | Number of candidate memory records considered, not four upper layers |
| Hard top-1 | Select one memory record, not only the top transformer layer |
| Five delta steps | Up to five optimization steps for a correction at a taught answer position |
| Eight PC iterations | Iterations of a settling calculation, not eight neural layers |
| `epc-50m` | A checkpoint from about 50 million training tokens |
| 3.35M reusable cap parameters | Stored network weights, excluding acquired record/delta memory |

The central picture is a **complete frozen 12-block language model with a selective external correction mechanism**. We tested choices about the correction mechanism's observations, learning rules and intervention sites. We did not show that the lower transformer blocks are unnecessary, nor distill the whole model into a cap that can operate on its own.

## Sources and verification

Implementation, checkpoint configuration and saved array shapes were inspected without importing JAX or running a model. The checked counts refer to model parameters, excluding stored causal-mask buffers. The links assume `assets` and `pc_cap` remain sibling directories.

1. [JAX GPT-2 implementation](../../pc_cap/src/pccap/bases/gpt2_jax.py): block structure, dimensions, shared embedding/output head, bank mapping and write placement.
2. [Local GPT-2 configuration](../models/gpt2/config.json): 12 layers, 12 heads, width 768 and vocabulary/position dimensions.
3. [Revision cap prediction and selection](../../pc_cap/src/pccap/revision_v1/learner.py): clean observation pass, cached prompt selection and corrected continuation.
4. [Full ordinary-text evaluation](../../pc_cap/scripts/r1_68f_full_validation.py): prefix-by-prefix evaluation policy.
5. [Reader networks](../../pc_cap/src/pccap/revision_v1/reader.py) and [observation extraction](../../pc_cap/src/pccap/revision_v1/observations.py): dimensions and branches. The latter's introductory “entering the tapped block” wording is imprecise; the base's actual retained states are **after** the named block, before the cap write, as implemented in source 1.
6. [Correction controller](../../pc_cap/src/pccap/revision_v1/controller.py) and [record acquisition](../../pc_cap/src/pccap/revision_v1/adapt.py): controller dimensions, explicit delta replacement and per-answer-position updates.
7. [Final learned-condition recipe](../../pc_cap/docs/tasks/R1-final-cell-recipes/61348508e40d54351613ab14.json): identity of the selected saved `theta_avg150-300.npz` used for the parameter count.
8. [Condition construction](../../pc_cap/src/pccap/revision_v1/stage4_adapters.py): main versus random settings, gates and acquisition configuration.
9. [Stable v0](../../pc_cap/src/pccap/revision_v1/v0_stable.py), [original v0](../../pc_cap/src/pccap/cap/cap.py) and [fixed key transformation](../../pc_cap/src/pccap/cap/features.py).
10. [PC reader-training implementation](../../pc_cap/src/pccap/revision_v1/epc_train.py): distinction between frozen-base computation and cap learning signals.
11. [Distillation driver](../../pc_cap/src/pccap/distill/train.py) and [pinned recipe](../../pc_cap/src/pccap/distill/recipe.py): teacher/student initialization, output supervision and token budget.
12. [PC graph](../../pc_cap/src/pccap/pc/nodes.py), [local weight update](../../pc_cap/src/pccap/pc/weight_phase.py) and [distillation objective](../../pc_cap/src/pccap/pc/kd_energy.py).
13. [Final ePC checkpoint state](../models/epc/epc-50m/checkpoints/final-009766/state.json): 50,001,920 tokens processed; parameter shapes were inspected in its companion `params.npz`.
14. [S1 interpretation memo](../../pc_cap/docs/R1_U03_interpretation_memo.md): literal self-distillation and ordinary-text continuation controls.
15. [Completed upper-layer report](../../pc_cap/docs/additional_work/AW-L_report.md) and [saved evaluation data](../../pc_cap/logs/additional_work/AW-L/report-round63-final/report.json).
