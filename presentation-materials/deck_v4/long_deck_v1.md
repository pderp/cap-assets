<!-- Editable slide source. Each --- starts a new page. HTML comments control layout and are not printed. All visible PDF text, including chart labels and numbers, comes from this file. Rebuild from pc_cap with: ../venv/bin/python -m aw.focused_long_deck -->

<!-- layout: cover; seconds: 45 -->
# 01 · Learning corrections without losing the rest
*1 / The research question*

Active Inference in the Extremes

Can a small adaptive memory improve a frozen language model while limiting the damage elsewhere?

charlie derr · research with Matthew Iklé

Colleague practice · 6 October 2026 · 35–40 minutes

> A working correction system, mixed predictive-coding results, and a useful bound on harm.

Source: Completed project results through 4 October 2026; presentation prepared 5 October.

---

<!-- layout: cards; seconds: 75 -->
# 02 · The original bet: make learning selective
*1 / The research question*

Attach a small learning system to a frozen transformer. Read its internal state, then add a bounded correction where it helps.

### Preserve useful knowledge
Learn a supplied answer without needlessly changing unrelated predictions.

### Share what should transfer
Recognize the same fact in different wording, while keeping nearby facts distinct.

### Test the mechanism and cost
Separate representation, learning signal and retrieval. Measure useful retention, interference and compute together.

> The first cap was motivated by predictive coding. Later experiments explicitly tested error inference.

Source: Original plan; Stage-4 report; corrected PC-v0, PC-v1 and PC-reader reports.

---

<!-- layout: cards; seconds: 105 -->
# 03 · Three ideas guided the programme
*2 / The motivating concepts*

We aimed to connect selective learning, decisions under uncertainty and the consequences of extreme errors.

### Active inference
Update beliefs and choose actions using a model of observations, preferred outcomes and information value. Our autonomous action-selection loop remains future work.

### Predictive coding
Use mismatches between predictions and observations to infer corrections. We tested iterative error inference in acquisition and reader training.

### Heavy-tailed distributions
Large deviations can remain more probable than an exponential tail predicts. We measured harmful prediction changes and tested tail descriptions over the observed range.

> The integration is incomplete. The experiments still reveal which components help, fail or cost too much.

Source: Presentation brief; completed additional-work report; HT-17 distribution analysis.

---

<!-- layout: flow; seconds: 90 -->
# 04 · What the cap actually does
*3 / Inside the experiments*

The main testbed uses GPT-2 small: 124 million parameters, with its base weights frozen.

### A new question
The transformer computes internal features. The cap reads features at blocks 4, 8 and 12.

### Memory and a reader
The reader compares the question with stored facts. A gate can select a correction or choose none.

### A corrected prediction
Bounded residual vectors are added at the write sites. The transformer produces its next-token probabilities.

> Frozen weights do not guarantee frozen behavior: changing an activation changes what happens downstream.

Source: Stage-4 implementation and report. Memory acquisition precedes these evaluation-time reads.

---

<!-- layout: cards; seconds: 80 -->
# 05 · Who supplies the answer to be learned?
*3 / Inside the experiments*

The targets were fixed in downloaded datasets before our runs. Our experiment did not invent replacement answers on the fly.

### zsRE: teach a reference answer
Prompt: “What league was Sporting Canamy?”

Target: Tercera División de México

We used the record's first reference answer, answers[0]. This is answer acquisition, not a deliberately false replacement.

### CounterFact: teach a controlled replacement
Prompt: “James Howell speaks”

Stored original: English · New target: Spanish

We used target_new from the record. Success means following the supplied edit; Spanish is not being asserted as historical truth.

> A dataset's original-answer label is separate from what our frozen model actually generated.

Source: Saved support examples zsre-train-14871 and cf-9366; downloaded zsRE and CounterFact records.

---

<!-- layout: table; seconds: 90; widths: 0.24,0.38,0.38 -->
# 06 · Does the answer survive different wording?
*3 / Inside the experiments*

Teach: “What league was Sporting Canamy?” → Tercera División de México

Test paraphrase: “What league did Sporting Canamy join with?”

| After 1,000 edits | Original prompt | Paraphrase |
| --- | --- | --- |
| Learned reader | Tercera División de México | Tercera División de México |
| Random reader | Tercera División de México | CD Atlético Baleares |
| Stable v0 cap | [empty answer] | forward |

The alternative question came from zsRE's rephrase field. During testing, the model saw the question without the target answer.

> Remembering the teaching prompt and recognizing the same request are different achievements.

Source: Saved realization 0, order 100. All three acquired this target immediately; this is one illustration.

---

<!-- layout: table; seconds: 75; widths: 0.25,0.25,0.50 -->
# 07 · A paraphrase can also add distracting context
*3 / Inside the experiments*

Teach: “James Howell speaks” → Spanish

Test: “Cataraqui is also the name of a municipal electoral district. The language used by James Howell is”

| After 1,000 edits | Original prompt | Paraphrase |
| --- | --- | --- |
| Learned reader | Spanish | Spanish |
| Random reader | Spanish | Ukrainian |
| Stable v0 cap | Spanish | "the city of the people." |

The entire test prompt came from CounterFact's paraphrase_prompts. We retained its unrelated opening sentence.

> We test the supplied alternative wordings. They are not a guarantee of understanding every possible question.

Source: Saved cf-9366, realization 0, order 100. Display removes leading spaces; this is one illustration.

---

<!-- layout: cards; seconds: 75 -->
# 08 · An edit must pass more than one test
*3 / Inside the experiments*

Generated answers stop at newline or end-of-sequence, with a 32-token limit. Editing scores use complete-answer matches to accepted variants.

### Acquire and retain
Can the cap produce the target now, and again after many later edits?

### Generalize the wording
Can it answer the supplied paraphrases? Retained paraphrase score is the main editing outcome.

### Preserve and revise
Do unrelated and nearby prompts retain the base's output? Can a newer answer replace an older one?

### Inspect probabilities
On ordinary text, compare the full token distribution and the probability of the actual next token.

> Preservation means preserving behavior. If the base gave a bad answer, preserving it is still a pass.

Source: Stage-4 scoring and checkpoint assays. CounterFact can average multiple paraphrases within an item.

---

<!-- layout: cards; seconds: 75 -->
# 09 · Recalling a fact is only the first step
*3 / Inside the experiments*

The two supplied papers help locate our work within a larger question: can a system use changed knowledge consistently?

### MQuAKE: consequences of an edit
The paper tests questions that require chains of facts after an edit. Our runs extracted single-fact changes from MQuAKE-CF and tested their alternative prompts at 300 edits.

### CounterBench: causal counterfactuals
The paper asks what follows when variables in an explicit causal system are changed. It studies causal inference, rather than simply recalling an edited association.

> We did not run CounterBench or MQuAKE's full multi-hop benchmark. Those remain stronger future tests.

Source: Zhong et al., MQuAKE, arXiv:2305.14795v3; Chen et al., CounterBench, arXiv:2502.11008v2.

---

<!-- layout: cards; seconds: 80 -->
# 10 · The central comparison changes the reader
*3 / Inside the experiments*

Same main-study base and supplied edit streams. These three conditions make the retrieval question easiest to see.

### Learned reader
A trained reader routes questions to the correction memory and can abstain.

### Random reader
Random-geometry retrieval with a gate tests how much the learned representation contributes.

### Stable v0 cap
The earlier activation-memory cap provides a reference for the newer reader architecture.

<!-- body -->
Three subject realizations × five orders. zsRE and CounterFact reach 1,000 edits; MQuAKE reaches 300 and is descriptive.

> Five orders reuse a realization's facts. They do not turn three subject populations into fifteen.

Source: Stage-4 triplet report; additional controls remain in the full report.

---

<!-- layout: metricbars; seconds: 75; maxima: 100,100,100 -->
# 11 · Learning the reader improves paraphrase retention
*4 / What we learned*

Retained paraphrase score, averaged over orders within each realization, then over the three realizations. Higher is better.

| Dataset and endpoint | Learned reader | Random reader | Stable v0 cap |
| --- | --- | --- | --- |
| zsRE · 1,000 edits | 96.0% | 52.4% | 18.6% |
| CounterFact · 1,000 edits | 67.8% | 12.1% | 0.0% |
| MQuAKE · 300 edits | 71.6% | 0.0% | 0.0% |

The learned-reader realization means span 95.5–96.5% on zsRE, 66.6–69.2% on CounterFact and 70.3–72.3% on MQuAKE.

> The cap often carries an answer beyond its teaching prompt. The strength of that transfer depends on the dataset.

Source: Stage-4 triplet summary. Bars start at zero on a common 0–100% scale; ranges are descriptive.

---

<!-- layout: cards; seconds: 75 -->
# 12 · Successful edits can still disturb other predictions
*4 / What we learned*

We replayed ordinary text at identical prefixes, comparing capped and uncapped predictions at 245,237 positions per cell.

### Distribution change: KL
KL compares the whole next-token probability distribution. All 45 main learned-reader cells exceeded the registered mean-KL limit of 0.001.

### Observed-token harm: Δ
Δ = log(p_base / p_cap) for the token actually present in the text. Positive values mean that token became less likely. Negative values are improvements.

### Why a small mean can mislead
Most positions change little. A small minority can suffer much larger losses. Measure how often, how severely and how far into the tail.

> The runs passed data-integrity checks. The learned reader failed the specified distribution-fidelity benchmark.

Source: Stage-4 report and HT-17. Positions share text windows and are not independent experimental replicates.

---

<!-- layout: metricbars; seconds: 80; maxima: 2.3,4.0 -->
# 13 · How often harm occurs and how large it is
*4 / What we learned*

Count a harmful change when Δ exceeds 0.01 nat. Severity is the mean Δ among those harmful positions.

| Dataset and cap | Harmful positions | Conditional severity |
| --- | --- | --- |
| zsRE · learned | 0.1594% | 1.630 nats |
| zsRE · random | 0.0266% | 1.806 nats |
| zsRE · stable | 0.1041% | 1.716 nats |
| CounterFact · learned | 0.2984% | 1.913 nats |
| CounterFact · random | 2.0450% | 3.486 nats |
| CounterFact · stable | 0.0000% | Undefined |

> Zero observed CounterFact harm for stable v0 accompanies zero paraphrase retention. Quietness alone is insufficient.

Source: HT-17; 15 cells per row, each with 245,237 positions. Both bar axes start at zero; units differ.

---

<!-- layout: survival; seconds: 80 -->
# 14 · Extreme losses have different observed tails
*4 / What we learned*

A survival curve shows the fraction of positions whose loss increase exceeds a chosen size. Farther right means a larger loss.

<!-- The following editable labels are drawn on the two-panel scientific plot. -->
### zsRE · learned reader
- Observed survival
- Saved exponential fit
- 0.01
- 0.1
- 1
- 10
- 0.1%
- 0.01%
- 0.001%

### zsRE · stable v0
- Observed survival
- Saved exponential fit
- 0.01
- 0.1
- 1
- 10
- 0.1%
- 0.01%
- 0.001%

<!-- body -->
Loss increase Δ (nats; logarithmic scale)

Fraction of all positions above that loss

> Stable v0 has a more pronounced tail here. The learned reader gains little from a more flexible tail fit.

Source: HT-17; illustrative realization 0, order 100; saved fits, no refitting. Finite-range evidence, not a tail law.

---

<!-- layout: flow; seconds: 80 -->
# 15 · A probability floor gives a bound we can prove
*4 / What we learned*

Mix the original next-token distribution with the cap's distribution at the same text prefix.

### Keep some of the base
ρ = exp(−1) ≈ 0.368

About 37% of the original distribution remains in the mixture.

### Add the corrected distribution
q = ρ p_base + (1 − ρ) p_cap

About 63% comes from the capped model.

### Bound the loss increase
q ≥ ρ p_base

log(p_base / q) ≤ 1 nat

> This bounds a token's loss at a shared prefix. It is not a one-nat bound on a whole generated answer.

Source: AW-B analytic mixture bound. The guarantee does not require a particular fitted tail family.

---

<!-- layout: metricbars; seconds: 80; maxima: 2.2,2.2 -->
# 16 · The mixture reduced severity to about one-third
*4 / What we learned*

Mean loss increase among positions with Δ > 0.01 nat, on ten exposed memories: two datasets × five orders at 300 edits.

| Dataset | Original cap | Probability mixture |
| --- | --- | --- |
| zsRE | 1.619 nats | 0.542 nats |
| CounterFact | 1.925 nats | 0.581 nats |

All ten memories met the declared retention-and-preservation rule. Paraphrase retention was unchanged on zsRE and fell by 0.67–1.17 percentage points on CounterFact.

Harm frequency barely changed. CounterFact mean KL still exceeded 0.001.

> This is a measured reduction in the severity of unintended changes, with a small editing trade-off.

Source: AW-B evaluation and HT-17. Mixture selected on development data; bars share a zero origin and scale.

---

<!-- layout: cards; seconds: 80 -->
# 17 · “Using predictive coding” has several meanings
*4 / What we learned*

Changing the base representation, the acquisition signal and the reader's training rule are separate interventions.

### Base representation
The legacy study uses a frozen 50M ePC base. The main study uses frozen 124M GPT-2. Results across these models are not a controlled representation comparison.

### Acquisition credit
Hold the base and reader fixed. Change the signal that tells a new memory correction which direction to move.

### Reader training
Hold the base fixed. Train the retrieval/controller network with backpropagation or iterative error inference, then acquire fresh memories.

> The next results isolate acquisition credit and reader training within their own paired experiments.

Source: Corrected PC-v0, fixed-v5 PC-v1 and PC-reader specifications and completed reports.

---

<!-- layout: cards; seconds: 90 -->
# 18 · What our error-inference experiment computes
*4 / What we learned*

Both acquisition arms start with the same target and use the same bounded memory-update rule.

### Adjoint credit
Differentiate the answer loss through the frozen model. Use the negative, normalized gradient to direct the correction.

### Error-inference credit
Hold existing writes fixed. Start temporary site errors at zero. Minimize a quadratic error penalty plus the answer loss, then normalize the inferred errors.

<!-- body -->
E(e) = ½ Σ ||e||² + answer loss with e

The default uses eight settling steps at rate 0.1. A one-step normalized update matches the adjoint direction to numerical tolerance.

> This implementation uses automatic differentiation. Its PC component is iterative error inference, not biological locality.

Source: Corrected PC acquisition implementation and one-step controls; all results shown use the repaired energy.

---

<!-- layout: metricbars; seconds: 85; maxima: 100,100,30 -->
# 19 · More settling bought retention at a cost
*4 / What we learned*

Legacy 50M ePC base with the v0 live cap: zsRE, three exposed realizations, order 100, after 1,000 edits.

| Settling steps | Original-prompt retention | Paraphrase retention | Learning time per cell |
| --- | --- | --- | --- |
| 1 | 51.5% | 13.1% | 5.7 min |
| 8 | 53.4% | 13.1% | 10.2 min |
| 32 | 56.5% | 12.2% | 25.4 min |

Mean ordinary-text loss increase rose from 0.00145 to 0.00221 nats between one and 32 steps. CounterFact paraphrase retention stayed at zero.

> More inference preserved more teaching prompts, but did not establish better transfer or lower harm.

Source: PC-controls report. Means over three realizations; timing is learning only, not whole-process time.

---

<!-- layout: table; seconds: 75; widths: 0.22,0.18,0.20,0.20,0.20 -->
# 20 · With the learned reader, credit effects were small
*4 / What we learned*

Frozen GPT-2 and the selected v5 reader; only acquisition credit changes. Each arm acquires 300 edits.

| Dataset | Credit | Paraphrase retention | Acquisition process | Largest token loss |
| --- | --- | --- | --- | --- |
| zsRE | Adjoint | 98.3% | 316 s | 9.26 nats |
| zsRE | Error inference | 98.3% | 426 s | 12.27 nats |
| CounterFact | Adjoint | 80.7% | 297 s | 11.74 nats |
| CounterFact | Error inference | 80.3% | 359 s | 12.23 nats |

Mean harm improved on zsRE and worsened on CounterFact. Small score differences are not proof of equivalent behavior.

> This transfer check provides no clear practical advantage for eight-step error credit.

Source: PC-v1; one exposed realization and order. Harm uses 245,237 positions; its separate readout cost is excluded here.

---

<!-- layout: metricbars; seconds: 80; maxima: 100,100 -->
# 21 · Training the reader with PC gave mixed outcomes
*4 / What we learned*

Three paired training seeds, the same 300 updates and 3.35M reader parameters. All evaluations use adjoint acquisition and 300 edits.

| Dataset and training seed | BP paraphrase retention | ePC paraphrase retention |
| --- | --- | --- |
| zsRE · seed 0 | 97.3% | 94.7% |
| zsRE · seed 1 | 99.0% | 97.0% |
| zsRE · seed 2 | 97.7% | 98.0% |
| CounterFact · seed 0 | 81.0% | 56.8% |
| CounterFact · seed 1 | 80.0% | 77.8% |
| CounterFact · seed 2 | 83.5% | 66.0% |

> CounterFact paraphrase retention fell in every pair. Its ordinary-text harm changed direction across seeds.

Source: PC-reader report, 12 completed evaluations. Training seeds reuse one subject population; bars share 0–100%.

---

<!-- layout: metricbars; seconds: 75; maxima: 26,26 -->
# 22 · The reader-training cost difference was large
*4 / What we learned*

Whole-training process time for the same 300 updates, including construction and caching. Each pair starts from matched parameters.

| Training seed | Backpropagation | Error-inference training |
| --- | --- | --- |
| Seed 0 | 0.241 h | 24.579 h |
| Seed 1 | 0.252 h | 24.112 h |
| Seed 2 | 0.242 h | 23.432 h |

Measured paired cost ratios: 102.1×, 95.8× and 96.7×. Backpropagation took about 14–15 minutes per reader; ePC took about a day.

> The installed ePC training procedure was substantially more expensive, without a consistent efficacy-and-harm gain.

Source: Completed PC-reader process receipts. Acquisition and evaluation are separate; bars share a zero origin and scale.

---

<!-- layout: metricbars; seconds: 75; maxima: 5,5 -->
# 23 · Last-layer writes increased measured harm
*4 / What we learned*

Last-only versus all-site writes, with readers using either all taps or the upper two. Bars show the ratio of mean signed loss increases.

| Dataset and training seed | All read taps | Upper read taps |
| --- | --- | --- |
| zsRE · seed 0 | 3.82× | 2.64× |
| zsRE · seed 1 | 3.38× | 2.71× |
| zsRE · seed 2 | 3.17× | 4.37× |
| CounterFact · seed 0 | 3.29× | 2.97× |
| CounterFact · seed 1 | 2.87× | 3.30× |
| CounterFact · seed 2 | 3.14× | 3.63× |

Upper-only reading also lowered CounterFact paraphrase retention in all three seeds.

> Every write restriction raised this harm measure, while paraphrase scores changed by at most 0.67 percentage points.

Source: AW-L, 24 evaluations including 6 shared controls. Ratio 1 means no change; readers were trained with full writes.

---

<!-- layout: cards; seconds: 85 -->
# 24 · What the experiments changed in our thinking
*4 / What we learned*

Useful retrieval, a good learning direction and control of collateral effects must be evaluated separately.

### Retrieval is central
Learning the reader greatly improves paraphrase retention. Restricting the interface to upper layers did not provide the hoped-for benefit.

### PC still has trade-offs
An adjoint control used 53–58% of its offered budget. Credit direction versus actual compute remains unresolved.

### A simple bound was useful
Mixing with the base reduced harmful-event severity while largely retaining edits. It did not solve every fidelity failure.

### The wider theory is still open
The bounded κ-loss pilot missed its success rule. That pilot did not implement the full coupled-entropy/free-energy proposal.

> The best next experiment should isolate one proposed mechanism and preserve both usefulness and harm as outcomes.

Source: Stage-4 and completed additional-work synthesis; PC-matched control; AW-B; κ-pilot interpretation.

---

<!-- layout: flow; seconds: 90 -->
# 25 · After the conference: make the blanket measurable
*5 / A more faithful next experiment*

A Markov blanket is a set of variables that makes internal and external states conditionally independent. Drawing a software boundary does not establish this property.

### Specify the states
Name the environment, the adaptive cap's internal state and the frozen transformer's state in a probabilistic model.

### Specify the interfaces
Define which observations enter, which corrections leave and what a proposed coupled or porous boundary actually asserts.

### Test the asserted property
Use a small controlled model with known dependencies. Measure residual dependence and perturb the interface before scaling up.

> The existing read/write interfaces are a starting point. A classical or coupled blanket requires its own stated test.

Source: Submitted abstract; abstract-to-testbed map; post-conference proposal. This work is proposed.

---

<!-- layout: cards; seconds: 85 -->
# 26 · Coupled entropy needs a complete objective
*5 / A more faithful next experiment*

The proposed framework changes how probabilities and rare states contribute to uncertainty. Replacing one loss function is only part of that specification.

### Define the distribution
Choose the modeled variable: correction state, residual or predicted token. Specify its support, normalization, units and reference distribution.

### Define the mathematics
Agree the coupled logarithm, normalized weighting, scale/root and constraints. Include their derivatives when optimizing the chosen free energy.

### Connect theory to a test
Recover the ordinary limit and check values and gradients against independent calculations. Then ask whether useful corrections cause less harm.

> A fitted tail shape is not automatically the objective's coupling parameter. Our earlier κ pilot did not test this full model.

Source: Nelson manuscript; coupled-objective note; post-conference collaboration proposal. Local JAX implementation proposed.

---

<!-- layout: cards; seconds: 85 -->
# 27 · First isolate the objective, then the learning rule
*5 / A more faithful next experiment*

Proposed first comparison: an agreed ordinary objective versus its coupled counterpart, using the same architecture and learning method.

### Pair the training
Three matched initializations, the same data and update schedule. Keep exact-gradient learning in both arms first, to isolate the objective's effect.

### Measure the trade-off
Evaluate both readers on the same two 300-edit streams: 12 cells. Report paraphrase retention, preservation, harm frequency, severity, extremes and actual cost.

### Extend only after that test
Add a matched predictive-coding comparison, then multi-hop or explicit causal tasks. Reused subjects support exploratory follow-up, not fresh confirmation.

> The question is whether the coupled objective improves the usefulness–harm trade-off, including when the answer is negative.

Source: Post-conference collaboration proposal. Timing and compute require a new local profile; no run has begun.

---

<!-- layout: flow; seconds: 75 -->
# 28 · Toward an agent that chooses what to investigate
*5 / A more faithful next experiment*

Active inference adds a decision: which observation or action is worth its cost, given current uncertainty and preferred outcomes?

### Observe
A correction arrives, a paraphrase fails or a nearby fact changes unexpectedly.

### Infer and choose
Model the uncertainty. Compare an audit, a correction and abstention by their expected consequences and information value.

### Learn and test
Use the result to update beliefs. Compare the policy with fixed or random audits at the same resource budget.

> For the conference talk: which result best explains the promise, and which limitation most needs a clearer explanation?

Source: Active-inference presentation brief and post-conference proposal. Autonomous policy selection remains proposed.
