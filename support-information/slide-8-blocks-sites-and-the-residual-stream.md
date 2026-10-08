# Slide "What a cap is": blocks 4, 8 and 12, the residual stream, and how a query flows through them

Prepared for charlie by Capstan, 2026-10-08. Companion to Capex's `gpt2-blocks-cap-layers-and-distillation.md`
(2026-10-07), which covers the full architecture and the cap's internal networks. This note answers two narrower
questions: what the residual stream is, and what actually happens to a query on its way to, through and past the three
sites. Everything here is read from the code that ran the experiments (`src/pccap/bases/gpt2_jax.py`, `hooks.py`,
`bp.py`, `revision_v1/learner.py`) and the calibration file `results/S2/residual_scales.json`.

## 1. The one-sentence version

GPT-2 small is twelve identical-shaped processing stages in a row. Every stage reads a running vector for each token,
computes something from it, and **adds** the result back onto that same running vector. That running vector, carried
from stage to stage with each stage's additions piled on, is the **residual stream**. The cap does nothing to the twelve
stages. It only adds its own small vector onto the running total at three of the eleven gaps between stages (after
stage 4 and after stage 8) and once at the very end (after stage 12), and only for the token position whose next token
is being predicted.

## 2. What a transformer block is, in just enough detail

A prompt is split into tokens. Each token becomes a vector of 768 numbers (its embedding plus a position embedding).
If the prompt has 20 tokens, the model carries 20 such vectors, one per position. Call the vector at position *i* after
block *l* `h_l[i]`. Before any block runs, `h_0[i]` is just the embedding.

One block does two things, each of which is an addition onto the vector it received:

```text
x  = h_{l-1}                                   (what arrived from the previous block)
x  = x + Attention(LayerNorm(x))               (positions mix: position i may look at positions ≤ i)
x  = x + MLP(LayerNorm(x))                     (each position processed on its own)
h_l = x                                        (what leaves for the next block)
```

That is the whole block (`gpt2_jax.py`, function `block`). Two details matter for the rest of this note:

- **Nothing is overwritten.** `h_l = h_{l-1} + (attention contribution) + (MLP contribution)`. If a block had nothing
  useful to say, it could add zero and the vector would pass through unchanged. The "plus the old value" wiring is the
  *residual connection*, and that is where the name residual stream comes from.
- **Attention is causal.** Position *i* can draw from positions 0 … *i* and never from later ones. So whatever happens
  at the last position cannot leak backwards into earlier positions' vectors.

After block 12 there is one more layer norm (`ln_f`) and a matrix multiply against the token-embedding table, which
turns the final 768-number vector at a position into 50,257 scores, one per vocabulary token. Softmax turns the scores
into next-token probabilities. For a prompt of *n* tokens the prediction we care about is the one made at the last
position, `p = n − 1`.

## 3. The residual stream, properly

The residual stream is the sequence `h_0[i], h_1[i], …, h_12[i]` for each position *i*: the same 768-slot vector,
read at the twelve gaps between blocks. It is useful to picture it as a conveyor belt running past twelve workstations:

```text
embedding ─► h_0 ─[block 1]─► h_1 ─[block 2]─► h_2 ─ … ─► h_4 ─ … ─► h_8 ─ … ─► h_12 ─► ln_f ─► scores
                     │                 │                   ▲           ▲           ▲
              adds to the belt   adds to the belt       site 1      site 2      site 3
```

Three properties follow directly from the "add, don't overwrite" wiring:

1. **Everything a later block sees is a sum of everything added before it.** Block 9 does not receive "block 8's
   output" in isolation; it receives the embedding plus all eight earlier contributions. This is why a vector added at
   the gap after block 4 is still present, in some form, at block 12: no later block can delete it, though each later
   block can add things that counteract or reinterpret it.
2. **The scale of the stream grows with depth.** Because contributions accumulate, the typical length of the vector
   gets longer as you go deeper. Measured on zsRE development prompts at the last position, the median vector length
   is about 68 after block 4, 104 after block 8, and 437 after block 12 (`residual_scales.json`, field `b_m`). The
   final layer norm removes this growth before scoring, which is why a vector added just before `ln_f` behaves
   differently from one added early (section 7).
3. **An addition at one gap and one position is a legitimate input to everything downstream.** The later blocks
   cannot tell whether a number in their input came from GPT-2's own earlier blocks or from the cap. That is the entire
   mechanism by which a cap write changes the answer.

## 4. Why blocks 4, 8 and 12, and why they are not special

The code fixes the sites by a rule, not by any property of those blocks: `l_m = round(m · 12 / 3)` for `m = 1, 2, 3`
(`hooks.py`). That gives one site a third of the way through, one two-thirds through, and one at the end. The same
rule on the six-block grammar base used in early testing gives sites 2, 4, 6. The design intent was to give the cap one
touch point in each third of the depth, not to single out blocks GPT-2 treats specially.

Two counting conventions appear in the records and both mean the same thing:

| Site (bank) | Human block number | Zero-based index in code (`BANK_BLOCK`) | Exact location |
| --- | ---: | ---: | --- |
| 1 | 4 | 3 | gap between block 4 and block 5 |
| 2 | 8 | 7 | gap between block 8 and block 9 |
| 3 | 12 | 11 | after block 12, **before** `ln_f` and the scoring matrix |

"After block 12" is a gap too, just the last one: there is no block 13, so a site-3 write is followed only by the
final layer norm and the score computation.

## 5. The flow of one query, step by step

Suppose a cap has decided to apply a record whose payload is three 768-number vectors `w_1, w_2, w_3`. The forward
pass (`run_blocks`) does this, for a prompt of *n* tokens with `p = n − 1`:

```text
h = embed(tokens)                             all n positions, 768 numbers each
for l in 1..12:
    h = block_l(h)                            ordinary GPT-2, all positions
    if l == 4:  record h[p]; h[p] = h[p] + w_1
    if l == 8:  record h[p]; h[p] = h[p] + w_2
    if l == 12: record h[p]; h[p] = h[p] + w_3
scores = ln_f(h[p]) @ embedding_tableᵀ        next-token scores at the last position only
```

Read it as a river with three places where a tributary joins:

- **To block 4:** the prompt is processed exactly as the frozen base would. Nothing from the cap has happened yet.
- **Site 1 (after block 4):** the cap *reads* the pre-write vector at position *p* (that is the "read" on the slide)
  and *writes* by adding `w_1` to that one vector. The other `n − 1` position vectors are untouched.
- **Through blocks 5 to 8:** these blocks run unchanged on the modified stream. Because only position *p* was
  altered, and position *p* is the last one, the attention of every earlier position is unaffected (causal mask). At
  position *p* itself, attention and the MLP now see a slightly different input and so add slightly different things.
  The write is being *processed*, not bypassed.
- **Site 2 (after block 8):** read the vector at *p* again (it now reflects both GPT-2's blocks 5 to 8 and the knock-on
  effects of `w_1`), add `w_2`.
- **Through blocks 9 to 12:** same again.
- **Site 3 (after block 12):** read, add `w_3`. This is the last chance to change the vector before scoring.
- **Past the sites:** `ln_f` and the scoring matrix. These are frozen too; they just convert the final vector at *p*
  into a probability over the next token.

So nothing flows *around* a block. There is no path that skips blocks 5 to 12 for a site-1 write; the write enters the
stream and is carried through every remaining block like any other content. The only "around" in the whole system is
the residual connection *inside* each block (section 2), which is GPT-2's own wiring and is what makes the stream
additive in the first place.

Two consequences that often surprise people:

- **A zero write is exactly the base.** Adding a zero vector is an exact no-op in floating point, so a cap that decides
  "no record applies" (the learned reader's null option) reproduces GPT-2's output to the bit. The slide's "a zero
  write reproduces the base exactly" is literal.
- **Nothing persists between queries inside GPT-2.** The writes are added to activations of this one forward pass. The
  next prompt starts again from embeddings. What persists is the cap's memory (the records), not any change inside the
  base.

## 6. One position only, and what that means for multi-token answers

Writes are applied at `p`, the last prompt position, and nowhere else (`bp.py` rejects any other position). That is
the position whose output is the next-token prediction, so it is the only position that matters for the answer.

A taught answer usually has several tokens ("Paris" might be one token; "the Eiffel Tower" is several). Generation is
greedy and one token at a time: the model predicts token 1, that token is appended to the prompt, the model runs again
on the longer prefix and predicts token 2, and so on. Each of those runs is a fresh forward pass with a new last
position, and the cap writes at *that* position. In the learned reader (v1), the record selection is made once from the
prompt and held for all answer positions, but the write vectors can differ per answer position: a record stores one
triple `(w_1, w_2, w_3)` per taught answer token, and when the answer runs past the taught length the cap stops writing
(`learner.py`, `predict`).

## 7. Why depth matters: what a write at each site can and cannot do

All three writes are 768 numbers, but they land in very different places.

- **Site 1 (after block 4)** has eight more blocks to pass through. The later attention and MLP computations at
  position *p* can transform it, amplify it, or cancel it. It is the most "indirect" lever: a small vector can be
  reinterpreted by a lot of frozen machinery before it reaches the scores. It is also the site where the stream is
  shortest (median length about 68 on zsRE), so a given absolute write size is relatively large.
- **Site 2 (after block 8)** has four blocks to pass through: a middle ground.
- **Site 3 (after block 12)** passes only through `ln_f` and the scoring matrix. It is the most direct lever on the
  output: close to "add this vector, get these score changes". But the stream here is longest (median about 437) and
  `ln_f` rescales the whole vector, so the write competes with everything GPT-2 has already accumulated.

The experiments bear on this directly. Writing only at site 3 (the "upper-layer interface" on the slide "Retrieval is
central") kept paraphrase retention within 0.7 points of the three-site cap but raised ordinary-text harm 2.6 to
4.4 times in every paired comparison: the direct lever is also the blunt one. The three-site design gives the cap an
indirect lever as well as the direct one.

The size budget on the slide is written relative to these depths. Each site has a reference scale `b_m` (the medians
above), and the v0 teaching procedure enforces `Σ_m ‖w_m‖ / b_m ≤ 0.3` (`cap/learn.py`; the learned reader's
acquisition uses the same kind of aggregate constraint): the three writes, each measured
as a fraction of the typical stream length at its own site, add up to at most 30 % of one typical vector. Without the
per-site scaling a budget of "0.3" would mean something six times stricter at site 3 than at site 1.

## 8. Reading before writing: how one query is actually run

Section 5 described a single pass with writes already in hand. The learned reader needs to look at the activations
*before* it can decide what, if anything, to write. The code does this with two passes rather than one (`learner.py`,
`predict`; `bp.py`, `forward_from`):

```text
Pass A (clean, no writes):
  embed ─► blocks 1–4 ─► blocks 5–8 ─► blocks 9–12 ─► ln_f ─► base scores
                 │ save h_4        │ save h_8      │ save h_12
                 └──────── reader looks at the last-position vector and the prompt-span mean
                           at each of the three sites, scores the stored keys, decides
                           "null" or "record r"

If null:   return the base scores from pass A.   (done; one full pass)

Pass B (corrected, resumed from the saved h_4):
  h_4[p] += w_1 ─► blocks 5–8 ─► h_8[p] += w_2 ─► blocks 9–12 ─► h_12[p] += w_3 ─► ln_f ─► scores
```

Pass B does not recompute blocks 1 to 4. Their output cannot have changed, because the first write happens after
them, so the saved `h_4` is reused and the block loop resumes at block 5 (`forward_from_jit` starts at
`BANK_BLOCK[bank] + 1`). This is why the cost ledger counts "one full forward plus one partial forward" per read.

The important conceptual point is that information read at site 3 (after block 12) can influence a write at site 1
(after block 4) only because there are two passes. Within a single pass information never flows backwards.

The stable v0 cap works site by site within one pass instead: each bank has its own key store, reads the vector at its
own site, fires if the key is within its radius, and adds its write before the next block runs. A site-1 write in v0
therefore changes what the site-2 bank reads. That is one of the reasons the two generations behave differently.

## 9. Where the error states of error predictive coding sit

The ePC base used for the error-inference credit adds an error variable at *every* block boundary, all twelve, on the
same residual stream (`bases/epc.py`). The three cap sites are three of those twelve boundaries (block indices 3, 7,
11). During settling the errors at all twelve boundaries relax; the credit handed to the cap is the settled error at
the three cap sites at position *p*. So "block boundary" on the slide "Error Predictive Coding" and "site" on the
slide "What a cap is" refer to the same kind of place, the gap between two blocks on the stream; ePC uses all of them,
the cap uses three.

## 10. Things the slide does not mean

- It does not mean GPT-2 has only blocks 4, 8 and 12, or that blocks 1 to 3 are skipped. All twelve run on every query.
- It does not mean the cap sits "on top of" block 12 as a thirteenth block. Site 3 is an addition at a gap, not a new
  stage.
- It does not mean the cap rewrites the whole sequence. One position, three vectors, one forward pass.
- It does not mean the base learns. The writes change activations for one query; the weights are untouched, and the
  next query starts from scratch.
- It does not mean a site-1 write "goes around" the later blocks to reach the output. It goes through them.

## Sources

1. `pc_cap/src/pccap/bases/gpt2_jax.py`: `block`, `embed`, `head`, `run_blocks`, `forward_jit`, `forward_from_jit`.
2. `pc_cap/src/pccap/bases/hooks.py` (`l_m = round(m·12/3)`); `docs/spec_defects.md` SD-7.
3. `pc_cap/src/pccap/bases/bp.py` (writes at position p only; pre-write sites; partial forward).
4. `pc_cap/src/pccap/revision_v1/learner.py`, `predict` (clean pass, selection held per query, resume from site 1,
   per-answer-position write vectors, no write beyond the taught answer).
5. `pc_cap/src/pccap/cap/learn.py` (`Σ‖Δv_m‖/b_m ≤ A`, A = 0.3); `cap/calibrate.py` and
   `pc_cap/results/S2/residual_scales.json` (b_m medians 68.08, 103.87, 436.92 on zsRE).
6. `pc_cap/src/pccap/bases/epc.py` (error variables at all twelve post-block residuals).
7. Deck slide "Retrieval is central" (last-site-only writes: paraphrase within 0.7 points, harm 2.6–4.4×); record in
   `pc_cap/docs/additional_work/AW-L_report.md`.
