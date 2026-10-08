# Speaking notes — 15-slide conference version

These notes support `main_deck.pdf` and `main_deck.pptx`. The allocations total **18 minutes before questions**, leaving two minutes of buffer within the 20-minute speaking limit and at least five minutes for discussion. They are planning estimates, not a timed rehearsal. Source links and optional answers follow the notes; they are not additional slides.

## 01 · Predictive coding cap experiments — 0:20

This is work with Matthew Iklé on whether a small adaptive system can learn useful corrections on top of a frozen language model. We will look at retrieval, predictive-coding learning signals, and the distribution of unintended prediction losses. Those are components of our active-inference programme, rather than a claim that the whole programme has already been implemented.

## 02 · The scientific question — 0:40

The practical question is easy to state: can we teach new answers without needlessly damaging what the model already does? The three themes have different roles. Active inference motivates a system that updates beliefs and chooses informative actions. Predictive coding offers a way to obtain learning signals through iterative error inference. Heavy-tail questions encourage us to inspect rare severe consequences, not only the average change. Our experiments measured the learning and preservation components. The autonomous action-selection part remains future work.

## 03 · What a cap is — 1:05

The base is GPT-2 small, with twelve transformer blocks and approximately 124 million parameters. A block is a stage in its computation. The cap can observe activations after blocks four, eight, and twelve, and add small correction vectors there. These are three access points to the same twelve-block model.

The memory holds corrections taught earlier. A reader decides whether a stored correction is relevant or whether the model should be left alone. In the main deployment, stored answer-position corrections are applied after retrieval; the cap is not retraining the entire language model for each new fact. Its own reusable machinery is fixed for an evaluated edit stream, while the correction memory grows.

Frozen weights do not imply unchanged predictions. An activation correction can change downstream computation. That is both how the cap helps and how it can cause collateral prediction changes. The experiment is local, on a small model; it establishes no transfer to production-scale models.

## 04 · Which reader? — 1:00

Stable v0 retrieves by fixed distance thresholds in activation space. The learned reader is trained to identify an applicable correction or choose none. The random-reader comparator uses untrained random geometry with its specified gate configuration. It is a useful control, but it is not literally identical to the learned reader with only its weights randomized: some enabled features and gate settings differ.

The key distinction is between storing a correction and finding it again under different wording. All these conditions can learn correction memories. The selected main-study learned reader was trained beforehand by ordinary backpropagation. Later I will distinguish changing the learning signal for a new correction from changing how the reader itself is trained.

## 05 · Teach, test, retest — 1:25

Each stream begins with an empty correction memory. We provide a prompt and target answer, teach that fact, and test it immediately without providing the answer. We then teach more facts and return to the earlier questions. We also ask held-out paraphrases: different wording seeking the same answer.

The main study used three fact samples and five orders of each sample. The zsRE and CounterFact streams reached one thousand edits; MQuAKE reached three hundred. In zsRE the target was the dataset reference answer. CounterFact supplied controlled replacement answers. Our MQuAKE payload used single-fact rewrites; this was not the standard multi-hop reasoning evaluation.

Usefulness means retaining the taught answer and recognizing it under new wording. Preservation has more than one test: unrelated factual prompts should retain their answers, and ordinary-text predictions should remain close to the uncapped base. These questions cannot be reduced to one accuracy score.

## 06 · Retrieval result — 1:35

Read the first three columns before the last one. Stable v0 retained every original prompt on CounterFact and MQuAKE, yet retained none of their paraphrases. On zsRE it retained about two-thirds of original prompts but fewer than one-fifth of paraphrases. Storing an answer is not enough to retrieve it under a new question.

The learned reader’s paraphrase scores were much higher: approximately 96 percent on zsRE, 68 percent on CounterFact, and 72 percent on the shorter MQuAKE stream. These are means over orders within each of three fact samples and then over those samples.

The footer uses a different comparison: the main three samples plus a supplemental fourth sample, comparing learned and random readers at one thousand edits. The learned reader’s paraphrase advantage was about 44 and 56 percentage points on zsRE and CounterFact. That extension strengthens the retrieval evidence; it does not replace the original registered classification. Next, the preservation qualifications matter.

## 07 · Preservation — 0:55

All forty-five learned-reader cells missed our registered mean-KL preservation limit. KL measures change in the full next-token distribution on ordinary text, not the percentage of wrong answers. The limit was 0.001 nats per token.

The CounterFact learned-versus-stable-v0 comparison was formally inconclusive because its locality requirement failed, despite the large paraphrase advantage. The MQuAKE stream is shorter and remains descriptive. We should report the useful retrieval improvement and these failures together. A less active reader can preserve ordinary text while failing to retrieve useful corrections; preservation alone is not sufficient either.

## 08 · Where PC enters — 1:40

When teaching an answer, we need to decide how to move the correction vectors. The adjoint method differentiates answer loss through the frozen transformer, takes the negative gradient, and normalizes its direction. The base weights remain fixed.

The error-based predictive-coding method introduces temporary error variables. It adjusts them repeatedly against a prediction-loss term and a quadratic error penalty. The settled errors at the write sites provide the alternative direction. Those iterations are settling steps, not added transformer layers.

Our digital error solver uses automatic differentiation through the graph. This is not evidence of a wholly local or backpropagation-free implementation. We are testing the resulting learning signal and its practical costs. The corrected comparisons shown here use the repaired error-only penalty; they are not the earlier defective-energy results.

There are two distinct interventions. We can keep the selected reader fixed and change how a new correction is acquired. Or we can change the learning estimator used when training the reader/controller, then evaluate each trained artifact using the same adjoint acquisition rule. The next two slides separate those experiments.

## 09 · Acquisition credit — 1:15

This comparison holds the selected reader and GPT-2 checkpoint fixed, and changes only the credit rule for acquiring three hundred edits. It is one exposed fact sample and order, not a new population-level confirmation.

The paraphrase results barely change: equal on zsRE and slightly lower with error inference on CounterFact. Process time rises. The final column is the largest token loss increase relative to the base, not the absolute token loss; both maxima increase. Mean harm is more mixed, improving on zsRE and worsening on CounterFact.

The timing column includes the whole cell process and is not pure learning time. This narrow comparison provides little evidence that the additional inference work bought useful retention here. Small numerical differences do not demonstrate equivalence, and these maxima alone do not summarize every aspect of harm.

## 10 · Training the reader — 1:35

This time we trained three paired seeds using BP or the corrected ePC estimator. Within each seed, initialization and training data sequences were matched. All readers were evaluated on the same exposed fact sample/order, with adjoint acquisition for the new facts. Three training seeds are not three new fact samples.

The table shows retained paraphrase accuracy. PC is lower in five of six pairs, including all three CounterFact pairs. Some harm measurements improve, particularly on zsRE, so the outcome is not a single scalar ranking.

The cost matters: ePC training took roughly twenty-three to twenty-five hours per seed, compared with about fifteen minutes for BP—approximately ninety-six to one hundred and two times longer for these completed runs. That is a result of this implementation and recipe, not a universal constant for PC. The 3.35-million-parameter count includes both reader and controller. This experiment does not establish a general failure of predictive coding, but it makes the practical trade-off clear for our setting.

## 11 · Settling depth — 1:00

This is a separate experiment using an older distilled checkpoint and live v0 cap. The base still has 124 million parameters. Fifty million denotes its approximate training-token budget, not its model size.

Across three fact samples in the same order, more settling increased original-prompt retention from about 51.5 to 56.5 percent. Paraphrase retention did not improve and fell at thirty-two steps. Learning time grew substantially, and mean ordinary-text loss increase rose too. The first error-inference step has the adjoint direction in exact arithmetic after normalization; tiny floating-point differences can remain.

The result is a limited benefit rather than no PC effect: more original prompts were retained, with costs and no broader wording benefit. If rehearsal runs long, this is the optional main slide to skip rather than rushing the distributional results.

## 12 · Observed tails — 2:00

First define the quantity on the horizontal axis. At a fixed text prefix, compare the loss assigned to the actual next token with and without the cap. Positive delta means the cap made that actual token less probable. Loss uses natural logarithms, measured in nats. An increase of one nat corresponds to a probability decrease by a factor of about 2.72.

The vertical axis is the fraction of all scored positions with a loss increase larger than the horizontal threshold. Both axes are logarithmic. This makes rare but severe changes visible. The two panels use the same ordinary-text inventory and show a fixed illustrative zsRE sample/order after one thousand edits. The text positions are dependent observations, not hundreds of thousands of independent experiments.

The solid lines are empirical survival curves. Dashed lines are the saved exponential fits to excesses above 0.01 nat. Stable v0 has a more pronounced tail than that exponential comparison predicts. For the learned reader, the more flexible tail fit added little held-out predictive value in the broader analysis.

This is evidence about finite observed ranges. It does not establish a power law, infinite variance, a complexity class, or a coupled-entropy parameter. Also, lower maxima need not imply lower averages among the worst losses. The reason to show this is that the frequency and severity of collateral effects deserve their own examination.

## 13 · Probability mixture — 2:00

We then asked whether an explicit bound could reduce severity while preserving useful editing. Mix approximately thirty-seven percent of the base distribution with sixty-three percent of the cap distribution.

For every token at the same prefix, the mixture contains at least the base’s thirty-seven-percent contribution. Its probability therefore cannot fall below that fraction of the base probability. Taking a negative logarithm yields the one-nat bound on loss increase. This is a mathematical guarantee for token likelihood relative to that base, not an empirical fit.

The table measures a separate quantity: average severity among positions whose loss increase exceeds 0.01 nat. That falls from about 1.6 to 0.54 nats on zsRE and 1.9 to 0.58 on CounterFact—approximately one-third of the original levels. These are ten exposed three-hundred-edit streams, a different population from the thousand-edit tail illustration.

Usefulness was largely retained: paraphrase retention did not change on zsRE and declined by about 0.7 to 1.2 percentage points on CounterFact. CounterFact still missed the mean-KL criterion. The mixture does not guarantee unchanged greedy answers; a mixture can change which token wins. Nor is one nat a bound on a whole answer, semantic harm, or separately generated continuations with different prefixes. It is a useful and precisely delimited intervention.

## 14 · What remains open — 1:30

The project has separated several questions that should not be conflated. Can a correction be found? Does a proposed learning signal improve the trade-off for its cost? What happens in the rare, severe part of the loss distribution?

The next active-inference step should add an actual decision: for example, selecting which uncertain fact to audit or update under a fixed budget. A specified policy could be compared with fixed or random selection while keeping usefulness, preservation, and cost as outcomes. We did not implement that autonomous policy in these experiments.

Likewise, a software interface is not proof of a probabilistic Markov blanket. The state variables and claimed conditional-independence properties need to be specified and tested. We welcome collaboration on a precise coupled-entropy model and an experiment capable of distinguishing its proposed mechanism. The limited κ-loss pilot was not a test of the full theory.

The existing measurements give us a concrete testbed for that work, with positive retrieval results, limited and costly PC effects, and an explicit bound on one kind of extreme loss.

## 15 · Questions — at least 5:00

Leave this slide visible for discussion. The QR code and short URL lead to charlie’s canonical presentation page, not an automatically published copy of this local alternative. The repository links provide experimental detail and materials. Acknowledge the collaborators and agentic assistance without using discussion time to read a list of roles.

## Evidence and optional answers

- Main retention and fidelity: [R1 triplet report](../../../pc_cap/docs/R1_stage4_report_triplet.md).
- Supplemental learned-versus-random result: [Option R report](../../../pc_cap/docs/additional_work/R_report.md). Four sample means, with the fourth supplemental; not a replacement registered classifier.
- Acquisition credit: [PC-v1 report](../../../pc_cap/docs/additional_work/PC-v1_report.md).
- Reader training, seed-specific harm and costs: [PC-reader report](../../../pc_cap/docs/additional_work/PC-reader_report.md).
- Settling depth: [PC-controls report](../../../pc_cap/docs/additional_work/PC-controls_report.md). Legacy harm inventory: 4,064 positions per cell, distinct from the main 245,237-position inventory.
- Tail analysis: [HT-17 report](../../../pc_cap/docs/additional_work/HT-17_report.md).
- Mixture and bound: [AW-B report](../../../pc_cap/docs/additional_work/AW-B_report.md).
- Upper-layer question: [AW-L report](../../../pc_cap/docs/additional_work/AW-L_report.md). Last-only writes retained paraphrases within 0.67 points but raised mean ordinary-text loss increase 2.64–4.37× in the twelve paired comparisons.
- Compute-matched question: [Matched-control report](../../../pc_cap/docs/additional_work/PC-matched-control_report.md). The extra-update adjoint arm consumed only 53–58% of its offered operation budget, so equal realized compute was not established.
- First-principles support: [nats](../../support-information/nats-from-first-principles.md), [architecture and distillation](../../support-information/gpt2-blocks-cap-layers-and-distillation.md), and [actual source examples](../../support-information/Capstan-README.md).

The linked source reports retain the qualifications and omitted experiments. No backup slides are appended to the 15-slide main PDF/PPTX.
