<!-- Editable slide source. Each --- starts a new slide. Layout comments are not displayed, except the page label. All visible PDF/PPTX text and chart labels come from this file. Speaker notes are separate. -->

<!-- layout: cover; seconds: 20; page: 01 / 15 -->
# Predictive coding cap experiments
*Active Inference in the Extremes · CCS 2026*

Learning corrections on a frozen transformer

charlie derr · Matthew Iklé

15 October 2026 · Binghamton, New York

> Retrieval, learning signals, and the consequences of extreme errors.

Source: Project results through October 2026.

---

<!-- layout: question; seconds: 40; page: 02 / 15 -->
# Can a small cap learn without disrupting the rest?
*The scientific question*

Teach a frozen language model new answers while preserving its other predictions.

### Active inference
The longer-term goal: update beliefs and choose informative actions.

### Predictive coding
Test whether iterative error inference provides useful learning signals.

### Heavy-tailed distributions
Ask whether rare, large losses change the story told by averages.

> We tested components of this programme. The full active-inference agent remains open.

Source: Submitted abstract; shared presentation brief; completed experiments.

---

<!-- layout: architecture; seconds: 65; page: 03 / 15 -->
# What a cap is
*The testbed*

GPT-2 small: 12 blocks, 124M parameters. Base weights stay fixed during the edit experiments.

### Frozen transformer
Prompt → blocks 1–12 → next-token probabilities

### Cap and memory
Read activations → retrieve a correction or abstain → add bounded write vectors

<!-- body -->
Read/write sites: after blocks 4, 8 and 12.

One local GPU; transfer to larger models is untested.

> No correction reproduces the base. Frozen weights can still produce changed behavior.

Source: Stage-4 implementation and architecture audit.

---

<!-- layout: readers; seconds: 60; page: 04 / 15 -->
# Which reader finds the correction?
*Separate retrieval from stored knowledge*

| Condition | Retrieval rule |
| --- | --- |
| Stable v0 | Fixed activation-distance thresholds select stored corrections. |
| Learned reader | A trained reader selects a relevant correction or chooses no correction. |
| Random-reader control | Untrained random geometry, with its specified gate configuration. |

The main learned reader was trained by backpropagation before these edit streams.

> Reusable reader weights stay fixed; the correction memory continues to learn.

Source: Stage-4 condition definitions; architecture/comparator audit.

---

<!-- layout: procedure; seconds: 85; page: 05 / 15 -->
# Teach, test, then retest after more learning
*What the experiment measures*

Teach a fact → test it now → teach more facts → retest earlier facts and paraphrases.

| Main-study dataset | Edits per stream |
| --- | --- |
| zsRE | 1,000 |
| CounterFact | 1,000 |
| MQuAKE | 300 |

### Usefulness
Does the original question—and a held-out rewording—still produce the taught answer?

### Preservation
Do unrelated questions retain their answers? How do predictions change on ordinary text?

<!-- body -->
Three fact samples, each tested in five orders. Our MQuAKE assay uses single-fact edits.

> Original-prompt retention and paraphrase retention answer different questions.

Source: Main-study protocol and triplet report.

---

<!-- layout: retention; seconds: 95; page: 06 / 15 -->
# Remembering a prompt is not enough
*Main study · retention at the final checkpoint*

| Dataset | Stable v0: original prompt | Stable v0: paraphrase | Learned reader: paraphrase |
| --- | --- | --- | --- |
| zsRE · 1,000 edits | 66.68% | 18.56% | 96.03% |
| CounterFact · 1,000 edits | 100% | 0% | 67.80% |
| MQuAKE · 300 edits | 100% | 0% | 71.56% |

Means across orders within each of three fact samples, then across samples.

Four-sample extension: learned versus random reader gained 44.1 points on zsRE and 56.2 on CounterFact in paraphrase retention.

> Learned retrieval greatly improved access to corrections under new wording.

Source: R1 triplet report; supplemental Option R report.

---

<!-- layout: preservation; seconds: 55; page: 07 / 15 -->
# Better retrieval did not meet every preservation goal
*Keep usefulness and preservation together*

### 45 / 45 cells
The learned reader exceeded the registered preservation limit: mean KL ≤ 0.001 nats per token on ordinary text.

### CounterFact
The comparison with stable v0 remained formally inconclusive because its locality requirement failed.

### MQuAKE
The shorter 300-edit run remains descriptive.

<!-- body -->
KL measures change in the full next-token probability distribution.

> A large paraphrase gain is not a complete preservation success.

Source: Main-study registered classification and fidelity results.

---

<!-- layout: credit; seconds: 100; page: 08 / 15 -->
# Where predictive coding enters
*Two ways to obtain a learning signal*

Teaching a fact needs a direction for changing its stored correction.

### Adjoint credit
Differentiate answer loss through the frozen transformer. Use the negative normalized gradient.

### Error-based PC credit
Relax temporary error variables against prediction loss and an error penalty. Use the settled site errors to direct the correction.

<!-- body -->
Our digital solver uses automatic differentiation through the graph.

We separately tested PC credit for acquiring facts and for training the reader/controller.

> PC is a tested learning mechanism here; autonomous action selection is still future work.

Source: Corrected ePC solver; PC-v1 and PC-reader specifications.

---

<!-- layout: acquisition; seconds: 75; page: 09 / 15 -->
# Changing acquisition credit gave little retention gain
*Fixed GPT-2 and selected reader · one exposed fact sample/order · 300 edits*

| Dataset | Credit | Paraphrase retention | Whole-process time | Max. loss increase vs. base |
| --- | --- | --- | --- | --- |
| zsRE | Adjoint | 98.3% | 316 s | 9.26 nats |
| zsRE | Error inference | 98.3% | 426 s | 12.27 nats |
| CounterFact | Adjoint | 80.7% | 297 s | 11.74 nats |
| CounterFact | Error inference | 80.3% | 359 s | 12.23 nats |

Mean harm moved in different directions across the two datasets. Small endpoint differences do not prove equivalence.

> This changes how facts are acquired; it does not retrain the reader.

Source: PC-v1 completed report; full ordinary-text inventory.

---

<!-- layout: reader_training; seconds: 95; page: 10 / 15 -->
# PC training reduced paraphrase retention in 5 of 6 pairs
*Three paired training seeds · same exposed fact sample/order · 300 edits*

| Dataset and seed | BP retention | ePC retention |
| --- | --- | --- |
| zsRE · 0 | 97.3% | 94.7% |
| zsRE · 1 | 99.0% | 97.0% |
| zsRE · 2 | 97.7% | 98.0% |
| CounterFact · 0 | 81.0% | 56.8% |
| CounterFact · 1 | 80.0% | 77.8% |
| CounterFact · 2 | 83.5% | 66.0% |

### 96–102× training time
ePC: 23–25 hours per seed. BP: about 15 minutes.

### Controlled comparison
300 updates; 3.35M reader/controller parameters. Every evaluation uses adjoint acquisition.

> Some harm measures improved, but PC was much more costly in this configuration.

Source: Completed PC-reader report. Training seeds are not new fact samples.

---

<!-- layout: settling; seconds: 60; page: 11 / 15 -->
# More settling improved original-prompt retention
*Older distilled base and live v0 cap · zsRE · 1,000 edits*

| Credit / settling steps | Original prompt | Paraphrase | Learning time |
| --- | --- | --- | --- |
| Adjoint reference | 51.5% | 13.1% | 4.6 min |
| Error inference · 1 | 51.5% | 13.1% | 5.7 min |
| Error inference · 8 | 53.4% | 13.1% | 10.2 min |
| Error inference · 32 | 56.5% | 12.2% | 25.4 min |

Mean ordinary-text loss increase rose from 0.00145 to 0.00221 nats between 1 and 32 steps.

124M-parameter base distilled over 50M training tokens. Three exposed fact samples, one order; a separate comparison from the main study.

> The original-prompt gain did not extend to paraphrases, and cost more time and harm.

Source: PC-v0 settling-depth controls. Learning time is a subset of total process time.

---

<!-- layout: survival; seconds: 120; page: 12 / 15 -->
# Extreme losses have different observed tails
*Why averages are insufficient*

Δ = loss with cap − loss without cap, at the same prefix. Positive Δ means worse prediction.

### zsRE · learned reader
- Observed survival
- Exponential excess fit
- 0.01
- 0.1
- 1
- 10
- 0.1%
- 0.01%
- 0.001%

### zsRE · stable v0
- Observed survival
- Exponential excess fit
- 0.01
- 0.1
- 1
- 10
- 0.1%
- 0.01%
- 0.001%

<!-- body -->
Loss increase Δ (nats; logarithmic scale)

Positions above threshold (log scale)

1 nat = a probability decrease by a factor of about 2.72. Fits use excesses above 0.01 nat.

> Stable v0 has the more pronounced tail here. A power-law family is not established.

Source: HT-17; fact sample 0/order 100; 1,000 edits; 245,237 shared text positions.

---

<!-- layout: mixture; seconds: 120; page: 13 / 15 -->
# A simple mixture bounds token loss increase
*Mathematical guarantee, measured usefulness*

p_mix = ρ p_base + (1 − ρ) p_cap, where ρ = e⁻¹ ≈ 0.37

At the same prefix: p_mix ≥ ρ p_base, so loss increase over the base is at most 1 nat.

| Conditional severity | Original cap | Mixture |
| --- | --- | --- |
| zsRE | 1.619 nats | 0.542 nats |
| CounterFact | 1.925 nats | 0.581 nats |

Severity averages positions with Δ > 0.01 nat. Ten exposed streams; 300 edits.

Paraphrase retention: unchanged on zsRE; down 0.7–1.2 points on CounterFact. CounterFact still missed the mean-KL limit.

> The guarantee bounds per-token loss increase; unchanged greedy answers are not guaranteed.

Source: AW-B probability-mixture experiment; HT-17 conditional-severity analysis.

---

<!-- layout: future; seconds: 90; page: 14 / 15 -->
# Toward active inference in the extremes
*What the results make possible next*

### Established components
We measured retrieval, PC learning trade-offs, and concentrated prediction losses.

### Open scientific step
Can an active-inference policy choose which facts to audit or update more effectively under the same budget?

<!-- body -->
Autonomous action selection and a tested probabilistic Markov blanket remain open.

We welcome collaboration on a precise coupled-entropy model and a discriminating experiment. The full coupled theory remains untested here.

> Evaluate usefulness, the learning mechanism, and extreme consequences together.

Source: Submitted programme; completed experiments; proposed future work.

---

<!-- layout: closing; seconds: 0; page: 15 / 15 -->
# Questions and discussion
*Active Inference in the Extremes · CCS 2026*

earthland.ai/ccs/

Canonical Google deck and presentation links

charlie derr · Matthew Iklé

SingularityNET · EarthLand · BGI Labs · TrueAGI

Predictive-coding implementation: FabricPC

Code: github.com/pderp/pc_cap

Materials: github.com/pderp/cap-assets

Agentic assistance: Capex · Capstan · Derp Peoples

> Which mechanism would you test next—and which failure would matter most?

Source: Scientific results and supporting material are linked from the project repositories.
