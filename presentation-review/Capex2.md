# Capex’s second presentation review

October 8, 2026. I fetched a fresh export of the [canonical Google deck](https://docs.google.com/presentation/d/1ofdKlNOS3n_cKVoS4Ga_81xDDU7Rt0_j8sSf2aVuPLg/edit), read all 30 slides, and inspected the rendered figures and tables. This review uses slide titles as well as current page numbers because the numbering will change. It also takes account of Capstan’s recent reviews. The speaking budget is **at most 20 minutes, with at least five minutes for questions**.

**The deck now explains much more of the experiment. I would shorten it by merging repeated explanations and conclusions, while retaining the experimental evidence.** The cap, learning-rule, and measurement definitions earn their time. The planning history, three separate introductions to PC, and five-slide “lessons learned” sequence are the strongest candidates for compression.

My recommendation is approximately **15 main slides, rehearsed to 18–19 minutes**. Keep the displaced details after the questions slide as backup. This preserves your ability to answer technical questions without giving every result a place in the spoken route. The suggestions below replace existing material; they are not additions to paste alongside it.

**The easiest cuts to make first**

1. **Combine the two opening slides (1–2).** Use “Predictive Coding Cap Experiments” as the title, the satellite name as a subtitle, and the authors beneath it. Keep the QR code prominent on the closing slide. There is no need to narrate two title screens.
2. **Move “This presentation was submitted as…” (3) to backup/resources.** Preserve the abstract, plan, and agent credits there. Explain the scientific ambition briefly on the objectives slide rather than walking through the project’s administrative origins.
3. **Remove “Datasets and repositories” (5) as a spoken slide.** Put the dataset names and stream lengths on the procedure slide; put repository links with the closing resources. The paragraph about the agent’s GitHub account can remain in acknowledgments.
4. **Fold “Scale and compute” (21) into the architecture caption.** “GPT-2 small, 124M parameters, one local GPU; larger-model transfer untested” supplies the essential scope. Keep the process-hour accounting in backup.
5. **Remove “Lessons learned” (22) as a transition slide.** Its announcement costs attention without advancing the argument. Put each lesson beside its evidence: retrieval beside the retention table, PC trade-offs beside the PC results, and the bound beside the mixture result.
6. **Merge “The wider theory is still open,” “Further work,” and “Coupled Entropy…” (26–28).** One final scientific slide can state the remaining gap and invite a specific collaboration. Keep your personal reflection as a brief spoken sentence if you want it.

These cuts require little redesign. Then make the following merges, which provide most of the remaining time savings.

**A complete shorter route**

| New position | Use these current slides | Treatment |
|---|---|---|
| 1. Title | 1–2 | One opening, with authors and session context. |
| 2. Scientific question | 4, with the ambition from 27 | Replace the paragraph with the short opening below. |
| 3. What a cap is | 8 + the scope from 21 | Retain the base/cap/memory distinction; shorten the prose. |
| 4. Which reader? | 9 | Three short definitions. Remove the oracle percentage, null threshold, and implementation detail from the spoken version. |
| 5. Teach, test, retest | 11–12 + dataset names from 5 | One procedure and measurement slide. |
| 6. Retrieval result | 13 + the retrieval result from 23 | Keep the current table; optionally carry the learned-versus-random result as one brief footer. |
| 7. Preservation trade-off | 14 | Three bullets replacing the paragraph. |
| 8. Where PC enters | 6–7 + 10 | One explanation of the actual credit comparison, immediately before its results. |
| 9. Changing acquisition credit | 15 | Keep the table, with corrected headings. |
| 10. Training the reader with PC | 16 | Keep the paired-seed table and the newly added training-cost comparison. |
| 11. What more settling changes | 20 | Keep a simpler table or move the full slide to backup if rehearsal runs long. |
| 12. Observed tails | 17 | Keep the figure and allow time to explain it. |
| 13. Bound and measured trade-off | 18–19 + 25 | One formula, the two-row severity table, and one retention/limitation sentence. |
| 14. What remains open | 26–28 | One concrete next question, with the full theory clearly untested. |
| 15. Questions and resources | 29–30, links from 3 and 5 | Closing QR/link, authors/affiliations and acknowledgments; no additional spoken tour. |

The upper-layer result from “Retrieval is central” and the offered-budget control from “Predictive Coding still has tradeoffs” belong in backup under this plan. They are legitimate findings, but each introduces another experimental design. Their omission from the main route does not require removing them from the shared deck.

For pacing, allow approximately 4½ minutes for slides 1–5, 2½ for 6–7, 4½ for 8–10, one for the settling result, four for the tails and mixture, and 1½ for the final scientific question: **18 minutes total**. This is a rehearsal target, not a measured duration. If you overrun, skip the settling-depth slide before rushing the tail figure or sacrificing questions.

**Short replacement text**

For **“More details about original objectives”**, replace the current paragraphs with:

> Can a small adaptive cap teach a frozen language model new answers without disrupting its other predictions?
>
> We tested retrieval, predictive-coding learning signals, and the distribution of unintended losses. These are components of our longer-term active-inference programme; the full agent remains to be built.

This also removes the awkward suggestion that continual learning itself “plagues” models. The difficulty is retaining useful behavior while learning new material.

For **“What a cap is”**, approximately halve the text:

> **Base:** GPT-2 small, 12 blocks and 124M parameters; its weights stay fixed during these experiments.
>
> **Cap:** reads activations and adds bounded correction vectors after blocks 4, 8, and 12.
>
> **Memory:** stores taught corrections. At query time, a reader retrieves a correction or abstains. No correction reproduces the base.

For **“Two generations of cap…”**, replace the paragraphs with three rows:

| Condition | Retrieval rule |
|---|---|
| Stable v0 | Fixed activation-distance thresholds select stored corrections. |
| Learned reader | A trained reader selects a correction or chooses no correction. |
| Random-reader control | Untrained random geometry, with its specified gate configuration. |

One sentence beneath the table suffices: **“The reusable reader is fixed during an edit stream; the correction memory continues to learn.”** The v5 checkpoint name can remain in technical captions. This avoids spending speaking time on naming conventions and removes an overstatement in the current random-reader description: its gate settings and enabled components are not identical to the learned condition. [Architecture/comparator explanation](../support-information/gpt2-blocks-cap-layers-and-distillation.md).

For the combined **procedure/measurement slide**:

> Teach one fact → test it immediately → teach more facts → retest earlier facts and their paraphrases.
>
> **Main study:** zsRE and CounterFact, 1,000 edits; MQuAKE, 300. Three fact samples, each tested in five orders.
>
> **Usefulness:** does the original question—and a held-out rewording—still produce the taught answer?
>
> **Preservation:** do unrelated questions retain their answers, and how do next-token probabilities change on ordinary text?

Move the detailed definition of Δ to the tail figure, where the audience needs it. Do not recite the entire inventory of metrics and thresholds in advance. If ES99+ remains on a displayed table, define it there as the average of the worst 1% of `max(Δ, 0)` values over all scored positions, including zeros; it is not simply the mean among harmful positions.

For **“Where PC enters”**, replace the three overlapping slides “Predictive Coding,” “Error Predictive Coding,” and “How an edit is taught and credited” with:

> Teaching a fact requires a direction for changing its stored correction.
>
> **Adjoint:** differentiate answer loss through the frozen transformer and use the negative normalized gradient.
>
> **Error-based PC:** repeatedly adjust temporary error variables against prediction loss and an error penalty; use the settled site errors to direct the correction.
>
> Our digital solver uses automatic differentiation. We separately tested PC credit for acquiring facts and for training the reader/controller.

This is shorter and more faithful to the experiment. In particular, delete the current claim that the transformer trains “without a single end-to-end backward pass.” Error relaxation differentiates through the graph, and the frozen-base acquisition experiment does not update each transformer block’s weights. The PC reader experiment also retains exact autodiff for retrieval and the reader/controller derivative. The two-phase description of historical transformer training should not be used as a description of all these experiments. [Solver](../../pc_cap/src/pccap/pc/epc_inference.py); [PC-reader specification](../../pc_cap/docs/additional_work/PC-reader.md).

For the **preservation paragraph after the first results table**, use:

> - Learned retrieval greatly improved paraphrase retention, but all 45 learned-reader cells missed the registered preservation limit: mean KL ≤ 0.001 nats per token.
> - The CounterFact comparison with stable v0 remained formally inconclusive because its locality requirement failed.
> - MQuAKE’s shorter run is descriptive.

Explain KL in one spoken sentence: “This measures how much the whole next-token probability distribution changed on ordinary text.” The original paragraph’s second explanation of stable v0 is already conveyed by the preceding table and can go.

For the combined **mixture slide**, retain the existing formula and two-row severity table, replacing the surrounding prose with:

> **A one-nat bound on token loss increase**
>
> `p_mix = e⁻¹ p_base + (1 − e⁻¹) p_cap`
>
> At the same prefix, token loss increase over the base is at most one nat.
>
> [Keep the current zsRE/CounterFact conditional-severity table.]
>
> Ten streams, 300 edits. Severity averages positions with Δ > 0.01 nat. Paraphrase retention was unchanged on zsRE and fell 0.7–1.2 percentage points on CounterFact; CounterFact still missed the mean-KL limit.

**One newly visible error needs correcting here:** the current sentence claiming that 63% cap weight preserves the greedy answer is false. A weighted mixture can change which token has the highest probability. The preservation of editing performance is measured, not guaranteed; the one-nat likelihood bound is the guarantee. Delete that sentence rather than qualifying it at length. As a simple check, a cap assigning probabilities 0.55/0.45 and a base assigning 0.10/0.90 produce a 63%/37% mixture near 0.38/0.62: the winner changes. [Bound and experimental results](../../pc_cap/docs/additional_work/AW-B_report.md).

For the merged **final scientific slide**:

> **Toward active inference in the extremes**
>
> We measured retrieval, PC learning trade-offs, and concentrated prediction losses. Autonomous action selection and a tested probabilistic Markov blanket remain open.
>
> Next question: can a specified active-inference policy choose which facts to audit or update more effectively under the same budget?
>
> We welcome collaboration on a precise coupled-entropy model and a discriminating experiment. Our limited κ-loss pilot did not test the full theory.

This retains the scientific gap and invitation while replacing three slides. If the κ pilot has not otherwise been explained, its sentence can move with the pilot details to backup. Keep the distinction between observed finite-range tails and an established heavy-tail family in the tail discussion; neither the plot nor the pilot establishes the full coupled theory.

**Small corrections to make during the compression**

| Current slide/title | Short correction |
|---|---|
| “Frozen GPT-2 and the selected v5 reader…” (15) | “Acquisition process” → **“Whole-process time”**; “Largest token loss” → **“Max. loss increase vs. base”**. Keep seconds/nats and the one-realization caption. The saved times and maxima need no numerical change. |
| “Training the reader…” (16) | “3.35M reader parameters” → **“3.35M reader/controller parameters.”** Keep the 96–102× training-time result already added. A clearer result title is **“PC training reduced paraphrase retention in five of six pairs.”** Harm outcomes remain mixed. |
| “More settling…” (20) | “Legacy 50M ePC base” → **“124M-parameter base distilled over 50M training tokens.”** The current caption still leaves model size ambiguous. |
| Tail figure (17) | Explain Δ as loss **increase**, and say these are observed finite-range tails. If changing the legend is easy, use **“Exponential fit above 0.01 nat.”** |
| “Further work” (27), if retained separately | “We didn’t actually create a true Markov blanket” → **“We did not specify and test a probabilistic Markov blanket.”** That reports what remains unestablished. |

The first two corrections follow the [acquisition-credit report](../../pc_cap/docs/additional_work/PC-v1_report.md) and [reader-training report](../../pc_cap/docs/additional_work/PC-reader_report.md). The training-token clarification is documented in the [architecture/distillation explanation](../support-information/gpt2-blocks-cap-layers-and-distillation.md).

I would not add another experiment, definition slide, or result table now. Give the existing tables conclusion-style titles, remove prose that repeats their message, and preserve time to explain the tail axes and why the probability bound works. Those explanations are likely to generate a better discussion than a faster tour of every completed experiment.

Reviewed snapshot: 30 pages, SHA-256 `79f7ff54fc4e4a1bd0e5789cee4e9e2406dfbe7cff89e0d1ead85d5a420f9112`. Later Google edits may supersede individual comments. The deck itself was not modified.
