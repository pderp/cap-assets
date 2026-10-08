# Capex’s review of Predictive Coding Cap Experiments

Reviewed October 8, 2026. Source: [Predictive_Coding_Cap_Experiments.pdf](../../Predictive_Coding_Cap_Experiments.pdf), all 24 pages, including the rendered tables and figures. Slide numbers below are PDF page numbers. I checked the principal scientific claims against our saved reports, implementation, and presentation brief, and read [Capstan’s review](Capstan.md) when it became available. This is feedback on the supplied deck; I have not changed it or run additional experiments.

**My assessment: there is a worthwhile conference talk here, but I would revise this version before presenting it.** The numerical results I checked agree with the research records. The main weakness is that an audience encounters results before learning what the cap does, which parts learn at which stage, and what the measurements mean. There are also several factual or labeling corrections, especially in the PC explanation. These can be addressed using existing evidence.

The scientific story I would emphasize is: we built a testbed for adapting a frozen language model; learned retrieval substantially improved access to stored corrections; predictive-coding credit produced limited benefits and substantial costs in the configurations tested; and looking beyond average performance exposed concentrated harm that a simple probability mixture could bound. That supplies substantive material for all three requested themes—active inference, predictive coding, and heavy-tailed distributions—provided the implemented components are distinguished from the broader active-inference proposal.

**Corrections I would make before the talk**

1. **Slides 6–7: replace the explanations of backpropagation and ePC.** Backpropagation computes derivatives; the optimizer updates the quantities selected for training. It does not require updating all weights. That distinction matters here because our transformer is frozen during the cap experiments.

   Local parameter-update rules in predictive coding also do not imply that learning needs no communication of errors through the network. In our implementation, optimizing the error variables uses automatic differentiation through the computation graph. Describing the experiment as avoiding backward computation would be misleading.

   The defining change in the cited ePC method is to optimize prediction-error variables and reconstruct network states from them. “Propagated via skip connections” is not an adequate explanation. Likewise, the depth limitation should be attributed to the canonical state-based formulation in digital simulation, rather than presented as a universal prohibition on deep PC. See the primary [ePC paper](https://arxiv.org/abs/2505.20137) and our [implemented solver](../../pc_cap/src/pccap/pc/epc_inference.py).

   Suggested replacement, focused on what we actually tested:

   > Backpropagation gives us a derivative telling us how a change would affect the prediction error. Our comparison method uses that derivative to choose a correction direction while keeping the transformer’s weights fixed.
   >
   > In error-based predictive coding, temporary prediction-error variables are adjusted over several settling steps. The resulting errors provide an alternative signal for learning. Our digital implementation still uses automatic differentiation; the experiment asks whether this iterative signal produces more useful corrections for its computational cost.

   Then distinguish **using that signal to acquire individual corrections** from **using it while training the reader/controller**. Neither experiment updates the frozen transformer’s block weights during the edit stream. This prevents the background explanation of PC weight learning from being mistaken for the actual treatment.

2. **Slide 11: correct both measurement labels.** The values 316, 426, 297, and 359 seconds are whole-process times, including construction/startup and stream execution. Rename “Acquisition process” to **“Whole-process time (s)”**. If you prefer to report learning time specifically, the learning-ledger values are 38.2 versus 138.8 seconds for zsRE and 22.4 versus 78.2 seconds for CounterFact; the numbers and heading would both need changing.

   Rename “Largest token loss” to **“Largest token loss increase vs. uncapped base (nats)”**. The displayed maxima are differences from the base, not absolute token losses. Add “one exposed realization, one order, 300 edits” to the caption. The values are correct, but their meaning and experimental scope need to travel with them. [PC-v1 report](../../pc_cap/docs/additional_work/PC-v1_report.md).

3. **Slide 12: distinguish the parameter count and show the training cost.** The saved package contains **3,348,228 reader/controller parameters**, comprising 1,640,964 reader parameters and 1,707,264 controller parameters. “3.35M reader/controller parameters” is the appropriate caption.

   The measured ePC training runs took **23.4–24.6 hours per seed**, compared with **14.4–15.1 minutes for BP**, approximately **96–102 times longer** in these 300-update runs. That is central evidence for the trade-off, not an optional implementation detail. It is a result for this implementation and configuration, not a universal speed ratio between PC and BP.

   “Mixed outcomes” is defensible across retention and harm, but the displayed retention table has a clearer message: ePC reduced paraphrase retention in five of six dataset/seed pairs, including all three CounterFact pairs. Some harm measurements improved, particularly on zsRE. Say both, rather than implying broadly balanced retention wins and losses. [PC-reader report](../../pc_cap/docs/additional_work/PC-reader_report.md); [parameter breakdown](../support-information/gpt2-blocks-cap-layers-and-distillation.md).

4. **Slide 15: write “124M-parameter base distilled over approximately 50M training tokens.”** “Legacy 50M ePC base” invites the interpretation that this is a 50-million-parameter model. It is not: this checkpoint has **124,439,808 parameters**, the same architectural count as GPT-2 small. The 50M denotes the training-token budget. Some earlier material I helped produce used ambiguous or incorrect wording here; this correction should propagate into the presentation too. [Architecture and distillation explanation](../support-information/gpt2-blocks-cap-layers-and-distillation.md).

   I would also sharpen the title to **“More settling improved original-prompt retention, but not paraphrase retention.”** The existing learning-time values—5.7, 10.2, and 25.4 minutes—are correctly labeled. Mean ordinary-text loss increase also rises across these depths, from 0.00145 to 0.00157 to 0.00221 nats. If this remains a main slide, mention that cost alongside time. Do not describe every harm statistic as increasing monotonically: the maxima do not. [PC-controls report](../../pc_cap/docs/additional_work/PC-controls_report.md).

5. **Slide 5: fix the CounterFact hyperlink.** It currently points to [CounterBench](https://arxiv.org/html/2502.11008v2), a different benchmark. Use [Locating and Editing Factual Associations in GPT](https://arxiv.org/abs/2202.05262), which introduced CounterFact, or the authors’ [ROME/CounterFact project page](https://rome.baulab.info/).

6. **Slide 21: describe the Markov-blanket result as unestablished.** A software boundary alone does not establish the required conditional-independence relationship. However, we also did not prove that no suitable probabilistic blanket exists. A more precise sentence is:

   > We built a software interface, but did not specify and test a probabilistic Markov blanket, or implement policy selection by expected free energy.

   This states the actual limitation without turning an untested property into a negative experimental finding. It follows the distinction in our [shared presentation brief](../../pc_cap/docs/presentation/presentation_brief_2026-09-26.md).

**Give the audience two foundations before the result tables**

First, show what the system is. One simple diagram can replace much of the early planning history: **prompt → frozen transformer → cap retrieves a correction or abstains → answer**, with a separate arrow showing how teaching adds a correction to memory. Label the transformer “GPT-2 small: 12 blocks, approximately 124M parameters.” Explain that the cap reads and intervenes after blocks 4, 8, and 12; those are access points, not three replacement transformer blocks.

The accompanying timeline should separate three operations:

| Operation | What changes? | What the listener should understand |
|---|---|---|
| Prepare the base and reusable cap machinery | Base preparation and reader/controller training occur before the evaluated edit stream | The older distilled checkpoint and the main GPT-2 checkpoint belong to different comparisons. |
| Teach successive facts during a stream | The correction memory learns; the base and the condition’s reusable machinery stay fixed | A “fixed cap” does not imply that its correction memory cannot acquire new entries. |
| Evaluate | Ask without supplying the target; score original prompts, paraphrases, and preservation | The cap-off model is the reference for ordinary-text probability changes. |

Use “stable retrieval cap,” “learned retrieval cap,” and “selected learned-reader checkpoint” before introducing the internal labels v0 and v5. Explain that stable v0 uses a fixed activation-based retrieval rule, whereas the learned reader was trained to choose relevant stored corrections or abstain. Keep the fuller distinctions in the [architecture guide](../support-information/gpt2-blocks-cap-layers-and-distillation.md) available for questions.

Second, show one real teaching example. For instance, the saved zsRE stream includes:

| Field | Actual saved value |
|---|---|
| Teaching prompt | What league was Sporting Canamy? |
| Target answer | Tercera División de México |
| Held-out alternative wording | What league did Sporting Canamy join with? |

This example lets you explain immediate success, remembering the original prompt after later edits, and recognizing a paraphrase. Its wording is supplied by the dataset, including the awkward phrasing. It is an illustration, not a representative statistical sample. [Saved example and outputs](../support-information/examples-zsre.md).

Also give each dataset one sentence of purpose. In our zsRE runs the target is the source’s reference answer; CounterFact supplies a counterfactual replacement; our MQuAKE payload uses supplied single-fact rewrites. We did **not** thereby evaluate the full standard MQuAKE multi-hop reasoning task. This matters more to understanding the experiment than three unexplained paper links. [Dataset-field provenance](../support-information/Capstan-README.md).

**Define “harm” before presenting its tails**

The audience needs to know what was damaged and what a nat measures. A usable explanation is:

> We also tested ordinary text unrelated to the taught facts. At each fixed prefix, we asked how much probability the model assigned to the actual next token. If adding the cap reduced that probability, the token became more surprising. We measured the increase in surprise using natural logarithms, in units called nats.

The technical definition can be a small formula:

`Δ = −ln p_cap(actual token | prefix) + ln p_base(actual token | prefix)`

Equivalently, `Δ = ln(p_base / p_cap)`. A positive value means worse likelihood for that token; one nat means its probability fell by a factor of about 2.72. This is a measure of **prediction degradation**, not a direct measurement of social or semantic harm. [First-principles explanation](../support-information/nats-from-first-principles.md).

Keep **mean KL divergence** separate: it compares the full next-token probability distributions, averaged across tested positions. The 0.001 threshold on slide 10 is our registered preservation criterion in nats, not 0.1% wrong answers and not the same statistic as mean observed-token loss increase.

Slide 13 is a useful figure once those quantities are defined. Explain its vertical axis aloud: “At each loss threshold, this tells us the fraction of all tested positions whose loss increase exceeded it.” Identify solid empirical curves and dashed exponential fits; the latter model exceedances above the chosen threshold. Add a compact caption identifying the illustrated zsRE realization/order and 1,000-edit endpoint. The approximately 245,000 scored positions are not independent experimental replications.

Preserve the current restraint about the tail claim. The data support **different observed finite-range tail behavior**: stable v0 on zsRE has a more pronounced tail than the exponential comparison predicts; the learned reader gains little held-out predictive value from the more flexible fit. This does not establish a power law, infinite variance, a universal complexity class, or a value of the coupled-entropy parameter κ. Nor does a lower maximum automatically mean a lower average of the worst losses. [HT-17 report](../../pc_cap/docs/additional_work/HT-17_report.md).

**Slide 14 can carry more of the talk’s scientific payoff**

The current severity values are correct, but “the mixture” is not defined before it is used. Add:

`p_mixture = e^(−1) p_base + (1 − e^(−1)) p_cap`

In ordinary language: combine about 37% of the base’s probability distribution with 63% of the cap’s. The mixture cannot assign any token less than `e^(−1)` times its base probability. Therefore, **at the same prefix, its token loss increase over the base is at most one nat**. This is an analytical bound, not merely the largest loss observed in a sample.

Then present the measured result already on the slide: conditional severity fell from 1.619 to 0.542 nats on zsRE and from 1.925 to 0.581 on CounterFact. Clarify that this averages positions above the 0.01-nat threshold separately for each condition; it does not mean every token’s loss fell by two-thirds or harmful-event frequency fell by two-thirds.

Pair that result with usefulness: paraphrase retention was unchanged on the five zsRE orders and fell by approximately 0.67–1.17 percentage points on CounterFact. All five CounterFact mixture cells still exceeded the 0.001 mean-KL criterion. The bound is relative to the specified uncapped base at a shared prefix; it is not a one-nat guarantee for an entire answer or a guarantee of semantic correctness. This makes a strong, properly limited conclusion: **we bounded a specific failure severity while largely retaining editing usefulness**. [AW-B report](../../pc_cap/docs/additional_work/AW-B_report.md); [conditional-severity analysis](../../pc_cap/docs/additional_work/HT-17_report.md).

**Keep the experiments distinct while simplifying the presentation**

These comparisons answer different questions. A short caption on each result is enough; the audience does not need our internal administrative history.

| Result | Changed quantity | Scope to keep visible |
|---|---|---|
| Main retrieval comparison, slide 9 | Cap/retrieval condition | Three subject realizations and five orders; 1,000 edits for zsRE/CounterFact, 300 for MQuAKE. The selected learned reader here is BP-trained. |
| PC acquisition, slide 11 | Credit rule with the selected reader fixed | One exposed realization/order, 300 edits. This does not retrain that reader with PC. |
| PC reader training, slide 12 | Reader/controller training estimator | Three paired training seeds, evaluated on the same exposed subject realization/order; adjoint acquisition in every arm. |
| Settling depth, slide 15 | Number of error-inference steps | Older distilled base with live v0 cap; three exposed realizations, one order; zsRE at 1,000 edits. |
| Mixture, slide 14 | Output probability distribution | Ten exposed memories: two datasets, five orders, 300 edits. |

In particular, three training seeds are not three new subject samples, and the legacy settling results are not a controlled comparison against the main-study base.

If you add one result, I would favor the learned-versus-random-reader evidence over another small ablation. The completed four-realization summary gives learned-reader paraphrase advantages of **44.1 percentage points on zsRE and 56.2 on CounterFact**. That comparison better supports the claim that learned retrieval matters than a comparison only against stable v0. Identify the fourth realization as a supplemental extension; it does not replace the original registered classification. [Option R report](../../pc_cap/docs/additional_work/R_report.md).

Conversely, slide 18’s “53–58% of offered budget” is too detached from its experiment. Either explain that an adjoint control was allowed additional acquisition updates but stopped before exhausting its operation allowance, or move this to backup. It is not GPU utilization, and it does not establish equal realized compute. [Matched-control report](../../pc_cap/docs/additional_work/PC-matched-control_report.md).

**Bring active inference into the opening and return to it at the end**

At present, active inference appears mainly as a resemblance to PC and an unfulfilled future ambition. That underuses the session context and charlie’s explicit three-theme brief. A short opening statement could be:

> Our longer-term aim is a system that updates its beliefs and chooses informative actions while controlling the damage from mistakes. Here we tested some ingredients: a small adaptive cap on a frozen language model, predictive-coding learning signals, and the distribution of unintended prediction changes. We have not yet built the full active-inference agent.

The missing step should then be concrete. The present experiment supplies edits externally. A future experiment could let the agent choose which uncertain fact to audit or update, using an explicitly specified model of preferences and information gain, and compare that policy with fixed or random choices under the same audit budget. That would test an active-inference contribution more directly than relabeling retrieval or externally supplied corrections as epistemic action. This is a proposed future direction, not a new run requested before the October 9 experimental cutoff.

Similarly, slide 20 should retain its explicit separation between the bounded κ-loss pilot and the full coupled-entropy/free-energy proposal. Failure of the former’s success rule does not refute the latter. If the pilot stays in the spoken talk, spend a sentence explaining what was changed and what failed; otherwise keep its details in backup. End with a concrete invitation: help specify the joint probabilistic model and a discriminating experiment for the proposed coupling mechanism. [Programme and scope](../../pc_cap/docs/presentation/presentation_brief_2026-09-26.md).

**Suggested treatment of the current slides**

| Slide(s) | Recommendation |
|---|---|
| 1–2 | Combine the opening. Distinguish the satellite title from the talk title; keep the submitted title available as a subtitle or short “submitted as” note. |
| 3 | Move detailed planning links and agent credits to acknowledgments/resources. Preserve attribution, but spend the opening on the scientific question. |
| 4 | State the question and implemented scope directly. Replace “continual learning, which plagues…” with “catastrophic forgetting during continual learning.” |
| 5 | Fix CounterFact’s link and explain what each dataset supplied in these runs. Add the concrete example. |
| 6–7 | Rewrite as above. Explain PC after introducing the cap, so the audience knows which learning problem it addresses. |
| 8 | Keep the sequential procedure, with a diagram and the preparation/acquisition/evaluation distinction. |
| 9 | Add a title such as “Remembering a prompt does not guarantee recognizing its paraphrase.” Define the columns before showing percentages. |
| 10 | Replace the pasted paragraph with three short points: paraphrase benefit; preservation failures; limits of the registered conclusion. Explain KL before citing 0.001. |
| 11 | Keep; correct the runtime and loss labels, identify the single exposed realization, and state the narrow acquisition-credit question. |
| 12 | Keep; correct the package label and include the approximately 100-fold training-time cost. |
| 13 | Keep as a central figure. Define the axes, quantity, population, and finite-range interpretation. |
| 14 | Keep; define the mixture and show both the analytical bound and measured retention trade-off. |
| 15 | Correct the 50M caption. Move beside the other PC results or to backup; do not return to PC abruptly after the tail/mixture conclusion. |
| 16 | Remove the announcement of the next four slides; use its substantive sentence as the transition or closing takeaway. |
| 17 | Keep the retrieval conclusion. If the upper-layer result stays, give its evidence; otherwise move that clause to backup. |
| 18 | Explain the offered-budget experiment or move it to backup. |
| 19 | Fold into slide 14 or the conclusion to avoid repeating a result without adding meaning. |
| 20 | Keep the narrow-pilot/full-theory distinction; provide minimal pilot context or reserve it for questions. |
| 21 | Replace broad disappointment with the precise untested active-inference/blanket properties and the next scientific question. |
| 22 | Preserve the invitation to collaborate, but shorten the paragraph and make the requested collaboration specific. The personal reflection can be spoken. |
| 23–24 | Combine affiliations/resources with the closing or keep them visible during questions. Add a short written URL alongside the QR code. |

For the approximately 15-minute conference version discussed earlier, I would budget roughly one minute for the question and active-inference programme, two for the architecture/example, 1.5 for the design and measurements, 1.5 for the retrieval result, three for PC methods/results, three for tails and the mixture, and two for conclusions and the next experiment. That is 14 minutes, leaving a small transition buffer. Detailed κ, upper-layer, settling-depth, and offered-budget results can serve as backup rather than competing for the same minute.

The visual improvement with the largest payoff is to replace screenshot tables with readable native text/graphics, give each result an explicit conclusion title, and retain only the numbers you intend to discuss. For PC training, paired seed points would expose the variation more quickly than the six-row table. For the mixture, the formula, one-nat bound, and a small before/after severity chart belong together. Reuse the existing architecture and example materials; new experiments are unnecessary for these revisions.

**Where my review agrees with, and qualifies, Capstan’s**

We agree on the wrong dataset link, the missing architecture/measurement explanations, the need to repair the PC description, the missing reader-training cost, and the unexplained offered-budget result. I would add the loss-increase label on slide 11, the reader/controller distinction on slide 12, and the explicit training-token interpretation of “50M” on slide 15.

I would not reuse “then updates each block’s weights” from Capstan’s proposed ePC description without clearly marking it as background about base training. It does not describe the frozen-base acquisition experiments shown here. Similarly, the main study’s ordinary-text inventory should not be carried over to the older PC-v0 controls: those use 4,064 scored positions per cell, whereas the main inventory has 245,237. These are small wording distinctions with substantial consequences for how a listener interprets the comparisons.

The PDF contains no speaker notes, so I cannot assess explanations charlie may already intend to give verbally. I also did not decode the QR code or verify every affiliation and agent-model label. Test the QR destination on a phone without a logged-in session, and ensure the final public deck is actually available there. My review concerns this PDF and the associated scientific record, not unseen revisions.
