# Understanding slide 24: what the experiments changed in our thinking

Prepared for charlie by Capex, October 6, 2026. This explains slide 24, “What the experiments changed in our thinking,” in [long_deck_v1.pdf](../presentation-materials/deck_v4/long_deck_v1.pdf). It expands each of the four cards from first principles and connects them to the experiments actually completed.

**The central lesson is that retrieving the right correction, learning a useful correction, and limiting unwanted changes are three distinct problems.** A method can improve one while making another worse. Slide 24 brings together several experiments that separated these questions; it does not describe a single system in which every proposed improvement was combined and tested.

## 1. The machinery behind the four cards

Our base language model predicts the next **token**, a piece of text. Before choosing a token, it assigns probabilities to all possible next tokens. The transformer's stored weights remain frozen during the edit streams.

A **cap** adds an editable memory and a mechanism for applying corrections to the transformer's temporary internal numerical states, called **activations**. Teaching a requested answer does not require changing the frozen transformer's weights.

Three activities need to be distinguished:

1. **Training reusable components.** A learned reader is trained to recognize when a query should use a stored correction. Its learned parameters can then be reused across many edit streams.
2. **Acquiring individual edits.** For each supplied prompt and target answer, the cap learns a correction and stores it in memory. Later edits accumulate in that memory. The experiments can change how these corrections are learned without changing how the reader was trained.
3. **Answering and evaluating.** A query retrieves a correction, if appropriate, and the model produces predictions. Some experiments additionally modify the final probabilities at this stage.

A **paraphrase** asks about a taught fact using different wording. Paraphrase retention asks whether the system still supplies the taught answer to those alternative questions after the edit stream. It tests whether a correction is useful beyond the exact sentence used to teach it. The reports abbreviate this score **RET-GS**. It averages item scores, which can include fractional credit across an item's paraphrases.

We also examine ordinary text that was not intended to be edited. At the same recorded text prefix, compare the probability of the actual next token under the base alone and under the cap. Define:

```text
Δ = log(base probability / capped probability)
```

Positive Δ means the cap made that actual token less likely. Negative Δ means it made the token more likely. Natural logarithms give units called **nats**. A Δ of 1 means the token became about 2.72 times less likely; it does not mean one additional wrong answer.

**KL divergence** measures a different thing: how much the entire next-token probability distribution changed. A model can give the same visible answer while its distribution changes. Our registered fidelity limit was a mean KL of **0.001**. This is separate from the mean signed Δ limit of **0.01**, and from counting individual positions whose Δ exceeds **0.01**.

The [slide-10 explanation](slide-10-stable-v0-training-and-baselines.md) expands the training timeline and cap variants. The [slide-12 explanation](slide-12-probabilities-fidelity-and-rare-harm.md) works through probabilities, KL, Δ and an actual extreme token-level change.

Here is where the slide's evidence fits:

| Slide card | What was varied or examined? | Stage of the system |
| --- | --- | --- |
| Retrieval is central | Learned versus other readers; then which transformer layers the cap reads and writes | Reusable reader and correction interface |
| PC still has trade-offs | How an individual correction receives its learning signal, with an additional compute allowance for the adjoint control | Acquiring edits |
| A simple bound was useful | Mix capped and uncapped next-token probabilities | Answering with already trained, already populated caps |
| The wider theory is still open | Change the loss used to train reusable cap components | An earlier training-objective pilot |

These studies used different experimental populations and, in the PC credit comparison, a different base model from the main GPT-2 study. Their numerical scores are not interchangeable measurements of one common treatment.

## 2. “Retrieval is central”

### Why recognizing the right question matters

Imagine storing a useful correction but applying it only when the user repeats the teaching prompt exactly. That system could succeed on the original prompt and fail on a paraphrase. Conversely, a permissive reader might apply the correction to a superficially similar question about a different subject.

The reader therefore has to generalize enough to recognize relevant questions and remain selective enough to reject irrelevant ones. The correction's usefulness depends on both its contents and where it is applied.

In the main Stage-4 comparison, average final paraphrase retention was:

| Dataset | Learned reader | Reader with random geometry | Stable v0 |
| --- | ---: | ---: | ---: |
| zsRE, after 1,000 edits | 96.03% | 52.40% | 18.56% |
| CounterFact, after 1,000 edits | 67.80% | 12.05% | 0.00% |

These are actual final-checkpoint means over the three realizations and five orders. zsRE supplies question-and-answer edits; CounterFact supplies counterfactual factual replacements. Stable v0 has fixed retrieval machinery while its correction memory still acquires edits. “Stable” does not mean an empty cap that never learns anything.

The large differences support investing in retrieval that recognizes paraphrases. However, the compared systems also differ in architecture and retrieval settings. This is evidence about the implemented systems, rather than a perfectly isolated estimate of changing only reader weights. The successful main learned reader was trained with ordinary backpropagation; its success alone is not evidence that predictive coding caused the improvement. [Source 1.]

### Why we tried upper layers

A transformer processes text through successive blocks. We wondered whether later representations would be more useful for recognizing factual meaning, while earlier representations might contribute distracting variation.

The completed **AW-L** experiment separated two changes:

| Choice | Broader interface | Restricted interface |
| --- | --- | --- |
| Where the cap reads activations | After blocks 4, 8 and 12 | After blocks 8 and 12 |
| Where it writes corrections | After blocks 4, 8 and 12 | After block 12 only |

All transformer blocks still ran. “Upper-only” did not mean removing the lower blocks or assuming that the base model could function without them. It meant restricting the cap's access points.

The four read/write combinations were evaluated on two datasets with three training seeds: **24 evaluations**, including six shared controls. A seed controls the random initialization used in training. Repeating across seeds checks whether an apparent result depends on one fortunate initialization.

Restricting writes to the last site increased the **mean signed Δ** in all 12 paired comparisons. The restricted/full-write ratios ranged from **2.64 to 4.37**. Paraphrase scores changed by at most **0.67 percentage points** within those write comparisons, and retrieval firing counts were unchanged. Thus, nearly unchanged visible editing scores did not imply nearly unchanged collateral effects.

That ratio concerns the cap-induced increment in token loss. It does **not** mean that the model made 2.64–4.37 times as many wrong answers, or that its total language-model loss multiplied by that amount.

Upper-only reading also lowered CounterFact paraphrase retention in all three seeds. With full writes, for example, seed 0 changed from **81.00% to 77.83%**. The zsRE results were mixed.

One limitation matters: readers were trained using the full-write objective; the experiment did not separately optimize a new reader/writer system specifically for last-site-only operation. The result argues against this particular restriction as an easy improvement. It does not establish that every possible upper-layer architecture must perform worse. [Source 2.]

**What changed in our thinking:** the earlier representations were not demonstrated to be disposable noise. Learning which correction applies remained valuable, and reducing the number of intervention sites did not automatically reduce unwanted effects.

## 3. “PC still has trade-offs”

### What a learning direction is

An individual correction contains many numbers. If a supplied answer is currently unlikely, which of those numbers should increase, which should decrease, and by how much?

That is a **credit-assignment** problem: work backward from the output error to identify changes that could reduce it. A learning direction is the proposed coordinated change to those numbers.

An **adjoint** calculation obtains a gradient using the chain rule through the model's computations. This is the ordinary reverse differentiation underlying backpropagation. Computing such a derivative through a frozen transformer does not update its weights; here it helps update the cap's correction.

**Predictive coding (PC)** instead uses prediction-error relationships among internal quantities, with iterative settling of temporary states. In the tested error-credit implementation, those settled states provide a correction-learning signal. The default comparison used **eight settling iterations**. Our implementation still uses automatic differentiation internally; “PC” should not be presented as “no derivatives or backpropagation anywhere.”

This supplemental credit experiment used the project's **50M ePC base and v0 live-key cap**, distinct from the main 124M GPT-2 reader comparison. It did not test PC training of the main learned reader. That was a separate supplemental study. [Sources 3–4.]

### Why offer the adjoint more computation?

If one method performs more internal work, a better answer could reflect that extra work as well as a better learning direction. We therefore tried an adjoint control allowed to spend as many counted learning operations on an item as the eight-iteration PC reference had spent on that same item.

The three names are:

| Name | Meaning |
| --- | --- |
| SE-A | Standard adjoint learning |
| SE-E | Error-credit PC learning, with eight settling iterations |
| SE-AM | Adjoint learning offered the per-item operation allowance measured in SE-E |

As charlie approved, the extra allowance could buy **additional acquisition updates**. It was not spent recalculating the same gradient at an unchanged correction simply to consume time.

An “operation” here is an accounting unit: a full forward pass, partial forward pass, or reverse pass each contributes one. These units do not assert equal hardware cost. A partial pass and a full pass can require different arithmetic. The allowance therefore was not an equality of elapsed GPU time or floating-point operations.

### Where 53–58% comes from

The saved control report records:

| Dataset and realization | Offered operations | Used operations | Used fraction |
| --- | ---: | ---: | ---: |
| zsRE, r0 | 391,311 | 225,484 | 57.62% |
| zsRE, r1 | 380,888 | 219,015 | 57.50% |
| zsRE, r2 | 388,261 | 225,589 | 58.10% |
| CounterFact, r0 | 61,344 | 32,996 | 53.79% |
| CounterFact, r1 | 62,026 | 33,456 | 53.94% |
| CounterFact, r2 | 61,096 | 32,628 | 53.40% |

This is the source of the slide's rounded **53–58%**. It is not GPU utilization, a percentage of facts learned, or the percentage of runs that finished.

Why leave computation unused? The control retained a stopping rule: stop updating when the supplied answer prefixes meet the learning threshold. It also stopped if the next operation would exceed that item's allowance. An unfinished update round was rolled back, while its computational work remained charged. Unused allowance for an easy item was not automatically transferred to another item.

In CounterFact, all **300 items per realization** stopped after attaining the threshold. In zsRE, **945, 953 and 962 of 1,000 items** respectively did so. Budget exhaustion and incomplete rounds also occurred in zsRE. These were completed runs following their specified stopping rules, not jobs that happened to terminate halfway through.

The extra-allowance control did not produce a broad improvement over standard adjoint. In zsRE, final paraphrase retention rose by **0.6–1.8 percentage points**, while final original-prompt retention fell by **0.2–1.2 points**. CounterFact's reported efficacy scores were unchanged.

The experiment answers what happened when adjoint was **offered** the PC allowance under these stopping rules. Because actual spending remained unequal, it does not isolate a PC advantage in direction quality at equal realized computation. That is what “credit direction versus actual compute remains unresolved” means. It neither establishes PC superiority nor rules out a useful PC method with a different formulation. [Sources 3–4.]

**What changed in our thinking:** compare what the methods actually spend and what they actually improve. An equal allowance on paper is insufficient to claim an equal-computation experiment.

## 4. “A simple bound was useful”

### This change happens after learning

The **AW-B** experiment restored saved learned-reader memories and changed how their predictions were combined with the base model's predictions. It did not retrain the reader or replace the correction-learning algorithm.

For every possible next token, at the same input prefix, the selected rule was:

```text
mixture probability = 0.367879 × base probability
                    + 0.632121 × cap probability
```

More precisely, the base weight is ρ = exp(−1), approximately 36.79%. The cap weight is 1−ρ, approximately 63.21%.

This combines **probabilities**. It does not choose the base's answer for 37% of questions, average two answer strings, or change 37% of the transformer's weights.

### Why this supplies a bound

Probabilities cannot be negative. Even if the cap gives some token an extremely small probability, the mixture still retains at least 36.79% of that token's base probability:

```text
mixture probability ≥ exp(−1) × base probability
```

For illustration only, if the base assigned a token probability 0.20, the mixture could not drive it below approximately **0.07358**. This is a fraction of its previous probability, not a rule saying every token gets probability at least 36.79%.

Taking the logarithmic ratio gives:

```text
Δ = log(base probability / mixture probability) ≤ 1 nat
```

The guarantee is mathematical, for each token at a **shared prefix** relative to that same base distribution. It is not just the largest change we happened to observe in the sample.

It also has a useful asymmetry: the mixture limits how far a token's probability can fall, while still permitting a large increase for an edited-answer token that the base originally considered very unlikely.

### What the experiment found

The mixture was selected using development memories, requiring retention within **two percentage points** of the unmodified cap on both datasets and no loss in the specified locality and near-miss checks. These check whether unrelated or deceptively similar prompts preserve their intended behavior. Eligible candidates were ranked by the smaller improvement across datasets in maximum harm, then in worst-tail average harm.

The selected setting was then evaluated on **ten already-exposed memories**: two datasets, five orders, realization 0, at 300 edits. This was supplemental evaluation on previously used populations, not ten independent new training seeds or a repeat of all main-study endpoints.

All ten memories met the declared combined rule: lower maximum and worst-1% positive harm, with retention within the two-point tolerance. zsRE paraphrase retention was unchanged in every order. CounterFact paraphrase retention fell by **0.67–1.17 percentage points**.

The largest observed token-loss increase among these unmodified memories was **15.38 nats**; all mixture maxima stayed below the theoretical **one-nat** ceiling, to numerical precision.

A companion analysis separated harmful-event frequency from severity. Among positions with Δ greater than 0.01, mean severity changed as follows:

| Dataset | Unmodified cap | Mixture |
| --- | ---: | ---: |
| zsRE | 1.619 nats | 0.542 nats |
| CounterFact | 1.925 nats | 0.581 nats |

The frequency above that threshold was almost unchanged. The principal benefit was reducing the size of the harmful changes, rather than eliminating all occasions on which they occurred. [Sources 5–7.]

### Why fidelity can still fail

A one-nat ceiling is not the same requirement as mean KL below 0.001. Many bounded changes can still leave the overall distribution too far from the base for the registered fidelity rule.

All five zsRE mixture memories had mean KL below 0.001. All five CounterFact mixture memories remained above it, with means approximately **0.00127–0.00195**. Thus, the bound was useful without making every memory pass fidelity.

Nor does the guarantee ensure correct answers, unchanged greedy decoding, or freedom from real-world harm. It limits a particular probability ratio. Over an N-token fixed reference continuation, the corresponding bound on the sum of token-loss increases is N nats, not one nat for the whole answer. Comparisons of two different freely generated histories need additional care because their prefixes differ.

Finally, no tested shrinkage or gate setting qualified as a comparator preserving efficacy closely enough on both datasets. We therefore cannot claim the mixture beat every alternative way of weakening a cap while holding usefulness fixed.

**What changed in our thinking:** directly constraining output probabilities can materially reduce extreme measured changes. It remains necessary to measure retention and average fidelity separately.

## 5. “The wider theory is still open”

### What the earlier κ pilot actually changed

The Greek letter **κ**, pronounced “kappa,” was a setting in an earlier training-loss experiment. A loss is the numerical penalty the optimizer tries to reduce while training reusable cap components.

Ordinary answer loss is **surprisal**, ℓ = −log p, where p is the probability assigned to a supplied target token. If p is small, the loss is large. The pilot replaced that answer-loss term with:

```text
Lκ(ℓ) = [1 − exp(−κℓ)] / κ
```

At κ = 0, the limiting formula is ordinary surprisal. For positive κ, the penalty flattens as surprisal grows:

| Setting | Largest possible answer-term penalty |
| --- | ---: |
| Ordinary, κ = 0 | No finite ceiling |
| κ = 0.2 | 5 |
| κ = 0.5 | 2 |

Flattening makes exceptionally unlikely target tokens exert less pressure on training. The derivative with respect to ordinary surprisal is exp(−κℓ), which decreases for larger ℓ. This can prevent extreme errors from dominating updates, but it can also make genuinely difficult target answers harder to learn. That is a mathematical explanation of a possible trade-off, not proof that it caused every observed pilot result.

The pilot also replaced the preservation KL term with a separately specified coupled divergence. In technical notation:

```text
Dκ(p || q) = Σᵢ pᵢ [(pᵢ/qᵢ)^κ − 1] / κ
```

Here p is the reference distribution and q the changed distribution. The implemented corrected form is nonnegative for normalized positive distributions and recovers KL in the zero-κ limit. The completed pilot used that corrected objective, not the earlier faulty preservation formula found during review. [Sources 8–9.]

**A bounded training answer term is not a bound on future prediction harm.** This distinction separates this card from AW-B. The pilot's preservation term need not be bounded, and the complete training objective and later token-level Δ do not inherit the answer term's ceiling.

### What “missed its success rule” means

The pilot completed **36 evaluations**: four objective settings, three training seeds and three datasets. The fourth setting clipped ordinary answer loss at 2. That ceiling matches κ = 0.5; it does not match κ = 0.2. The clipping control also retained ordinary KL preservation, so the comparison is not a change of answer-loss shape alone.

The aggregate results were:

| Training objective | Paraphrase retention | Average worst-5% positive harm, ES95 |
| --- | ---: | ---: |
| Ordinary | 79.61% | 0.22292 nats |
| κ = 0.2 | 75.44% | 0.08364 nats |
| κ = 0.5 | 74.78% | 0.06348 nats |
| Clipped ordinary loss at 2 | 77.89% | 0.10327 nats |

These are equal-dataset averages within each seed, then averages across seeds. **ES95** means the average of the worst 5% of the positive-part token-loss changes; improvements are set to zero when forming that distribution. It is not the same statistic as the worst-1% ES99 used elsewhere. These historical pilot measurements used a smaller ordinary-text inventory than the later full-validation assays, so the columns should not be compared numerically with main-study tail summaries as if their populations matched.

There really were lower measured tail averages. “Missed” does not mean “nothing changed.” The agreed rule also required retention within two percentage points of ordinary, non-increasing unwanted firing on unseen prompts in each dataset, and tail improvements large enough to exceed the specified across-seed spread criterion.

The retention floor was **77.61%**. Both κ settings fell below it. Their lower ES95 and maximum-harm averages also failed the seed-spread separation criterion: results varied too much across the small set of seeds for that rule to declare the desired improvement. This was a descriptive pilot rule, not a confirmatory significance test.

The clipped control passed retention but failed the unseen-firing condition on CounterFact and also failed tail separation. It was not a successful all-criteria alternative. [Source 8.]

### Why this does not settle the coupled-entropy proposal

The broader proposal concerns how a probabilistic agent represents uncertainty and averages information or energy across possible states. Changing one token-loss function is only one possible ingredient.

In an ordinary expectation, we average quantities using their probabilities. A **coupled expectation** can instead use transformed, renormalized probability weights, sometimes called an **escort distribution**. Both what is being averaged and how the averaging weights change matter. The earlier pilot did not implement the full proposed normalized expectation or a changed inference distribution.

A full **free-energy** formulation additionally needs an explicit probabilistic model: what the hidden states are, how they produce observations, what prior beliefs apply, and how the agent represents uncertainty about those states. Here “free energy” is a mathematical objective for inference, not GPU electricity consumption.

An **active-inference** experiment would further specify available actions, preferences, predicted consequences and an action-selection rule. For example, selecting which fact to audit for expected information and usefulness could be an action. Merely updating a supplied correction or limiting a probability change does not demonstrate that policy mechanism.

Consequently, the pilot does not confirm or refute the full coupled-entropy/free-energy framework. It shows what happened under the particular bounded-loss and preservation-divergence recipe that was implemented. The later mathematical calibration work and proposed coupled objective remain separate from demonstrated improvements in the cap. [Sources 10–11.]

### How this relates to heavy tails

The harm measurements ask whether rare, large changes matter and what their measured distribution looks like. A few severe observations can dominate total damage even when a typical observation changes very little.

That observation alone does not establish a particular heavy-tailed probability law. Nor is the κ used as a training-loss setting automatically the same parameter as a fitted shape parameter for measured harms, or the κ of a proposed latent-state model. Those connect different mathematical objects and require an explicit argument.

The mixture's one-nat ceiling is especially clear: it follows from its formula regardless of which tail model best describes the unmodified cap. We did not need to prove a heavy-tail law to obtain that protection. [Sources 7 and 10.]

**What changed in our thinking:** a lower tail statistic is insufficient if useful learning deteriorates, and a negative result for one loss recipe cannot settle a broader theory that recipe did not implement.

## 6. What the final sentence proposes

“Isolate one proposed mechanism” means asking a question narrow enough that the result has a clear interpretation.

For example, a future coupled-objective test could use the same base, cap architecture, data, paired initializations and edit-acquisition procedure, while changing the fully specified training objective. First check its mathematical limits and gradients; then measure whether it retains edits, recognizes paraphrases, avoids unwanted firing, controls rare severe changes and uses reasonable actual computation.

Changing the objective, architecture, PC learning rule, data and output bound simultaneously could produce an interesting system, but would make it difficult to determine which change helped. PC training and active selection of audits can be tested as additional mechanisms once their comparisons are defined.

This is the reasoning behind the documented future proposal, not a claim that those experiments have run or that this explanatory supplement authorizes another GPU job. [Source 11.]

## 7. A spoken explanation of the whole slide

> “These experiments made us separate three questions: can the cap recognize when a correction applies, can it learn that correction efficiently, and can it avoid disturbing other predictions? Learning the reader was valuable, but restricting access to upper layers was not the easy improvement we hoped for. Our predictive-coding comparison still leaves a compute question open, because the adjoint control used only about half the allowance it was offered. A simple mixture with the original model gave us a real mathematical limit on individual probability damage and largely preserved edits, although some average fidelity tests still failed. Finally, our earlier kappa-loss pilot lowered tail measures but lost too much useful retention. It also wasn't an implementation of the full coupled-entropy theory. The next experiment should test a clearly specified mechanism and keep usefulness, unwanted changes and actual cost visible together.”

## Sources and verification

The relative project links below work when `assets` and `pc_cap` are sibling directories, as they are here. Experimental numbers come from the saved reports and machine-readable summaries; the small probability-floor example is explicitly illustrative. No new model execution was needed.

1. [Stage-4 comparison report](../../pc_cap/docs/R1_stage4_report_triplet.md) and [final comparison data](../../pc_cap/logs/R1/reports/triplet/summary.json).
2. [AW-L completed layer-interface report](../../pc_cap/docs/additional_work/AW-L_report.md) and [24-evaluation data](../../pc_cap/logs/additional_work/AW-L/report-round63-final/report.json).
3. [PC matched-allowance control report](../../pc_cap/docs/additional_work/PC-matched-control_report.md) and [implemented budget/stopping rules](../../pc_cap/aw/pc_matched_credit.py).
4. [Corrected PC-v0 credit comparison](../../pc_cap/docs/additional_work/PC-v0_report.md) and [PC-v0 specification](../../pc_cap/docs/additional_work/PC-v0.md).
5. [AW-B calibration and evaluation report](../../pc_cap/docs/additional_work/AW-B_report.md) and [selection/evaluation data](../../pc_cap/logs/additional_work/AW-B/report-20260929/report.json).
6. [Mixture and other probability transformations](../../pc_cap/aw/bounded.py).
7. [HT-17 distributional interpretation](../../pc_cap/docs/additional_work/HT-17_report.md).
8. [Completed historical κ-pilot report](../../pc_cap/logs/r1_round18/ht3d-pilot-final-aliases.md) and [pilot aggregates and decision checks](../../pc_cap/logs/r1_round18/ht3d-pilot-final-aliases.json).
9. [Implemented κ answer loss and corrected preservation divergence](../../pc_cap/src/pccap/revision_v1/train.py) and [objective review and repair record](../../pc_cap/docs/tasks/HT-3b.md).
10. [Coupled-objective specification and mathematical calibration note](../../pc_cap/docs/additional_work/coupled_objective_note.md).
11. [Post-conference collaboration proposal](../../pc_cap/docs/post_conference/coupled_collaboration_proposal.md).

The [verification record](../../pc_cap/logs/presentation/slide-24-lessons-20261006/verification.json) binds the consulted sources and checks the displayed numerical comparisons and links. The presentation itself and experiment files are unchanged.
