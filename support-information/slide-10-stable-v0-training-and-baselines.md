# Understanding slide 10: stable v0, cap training, and the frozen-model baseline

Prepared for charlie by Capex, October 5, 2026. This explains slide 10, “The central comparison changes the reader,” in [long_deck_v1.md](../presentation-materials/deck_v4/long_deck_v1.md). It describes the experiments actually run, using their saved recipes, code and results.

The key distinction is between **learning how to find a correction** and **learning a particular correction**. The learned reader does both, at different times. Stable v0 learns particular corrections during the experiment, but uses a fixed mathematical rule to find them. In all three conditions on slide 10, the underlying GPT-2 model keeps the same pretrained weights.

“Stable” describes the source of v0's retrieval keys. It does **not** mean that its correction memory never changes, that its answers always remain stable, or that it cannot forget an earlier edit.

## The three things that can be called “training”

A transformer has permanent numerical **weights**, and it produces temporary numerical **activations** while processing a particular piece of text. Our caps change activations during a prediction and store correction vectors outside the transformer. They do not rewrite GPT-2's weights in the three slide-10 conditions.

There are three different learning stages:

| Stage | What happened in this study | What was subsequently kept fixed? |
| --- | --- | --- |
| Base-model pretraining | We started with an already pretrained GPT-2 small model, approximately 124 million parameters. We did not train this main-study base from scratch. | Its weights stayed fixed throughout the three slide-10 conditions. |
| Reusable cap training and calibration | Before the final edit streams, the learned reader was trained on separate development/training material. Random geometry was initialized and retained without that reader training. Stable v0 used a fixed key transformation and previously calibrated retrieval radii and write scales. | Reader/controller weights and the chosen settings were fixed for final evaluation. |
| Acquiring the particular edits | During each experimental stream, every cap was given an original prompt and its supplied target answer. It learned correction vectors and stored them in its own memory. | At each subsequent test, that memory was read without learning from the test answer. Acquisition resumed when the next edit arrived. |

Thus “frozen base” and “the cap is learning” are compatible. We use derivatives through the base to discover useful activation corrections, while leaving the base's own weights untouched. Computing a gradient through a model does not require updating that model's weights.

## The actual sequence within a run

For a particular dataset, subject realization and ordering, each condition followed this sequence:

```text
Load the same frozen GPT-2 base
    |
Attach this condition's fixed machinery and an empty correction memory
    |
Teach edit 1 using its original prompt and target answer
    |
Ask its original prompt without supplying the answer; record immediate success
    |
Teach edit 2, test it, teach edit 3, test it, ...
    |
At the scheduled checkpoints, test the accumulated memory and preservation
    |
Continue to 1,000 edits for zsRE/CounterFact, or 300 for MQuAKE
    |
Test earlier original prompts and their paraphrases using the final memory
```

The checkpoints were 100, 300 and 1,000 edits for zsRE/CounterFact, and 100 and 300 for MQuAKE. A checkpoint at 300 is a continuation of that run's first 100 edits, not a fresh training run. A different ordering starts a separate memory; it does not inherit the preceding ordering's corrections. Restoring an interrupted run restores that run's own state.

The three caps are **parallel experimental alternatives**. We did not first train stable v0, hand its filled memory to the random reader, and then hand that memory to the learned reader. Each acquired the same supplied edits independently. Nor are the three attached simultaneously as a stack.

There were three subject realizations and five orderings per realization: 15 memories per dataset and condition, or 45 per condition over the three datasets. The five orderings within a realization reuse its facts. These are not 15 independently trained readers or 15 independent subject populations.

At evaluation, the model receives the question, not the target answer. The target is available to the scorer after generation. The final-stream paraphrases are tests, not additional teaching examples for those edits. Earlier reusable-reader training did include paraphrases of its training material; that is a different stage.

Near-miss and revision challenges are a small exception to “evaluation is read-only”: they deliberately teach extra challenge edits in a saved-and-restored copy of the current state. Those challenge edits do not remain in the main stream's memory. The individual test predictions remain read-only. [Sources 1–3 below.]

## What stable v0 actually stores and does

Imagine a correction memory with an **address** and an **instruction** in each slot:

- The address, called a **key**, describes the transformer's internal state for a particular text prefix.
- The instruction, called a **value** or **write**, is a vector to add to the transformer's activations when that address is recognized.

This is an analogy to a lookup table, but the matching is numerical. The slot is not simply a dictionary entry mapping an English question to an answer string.

For GPT-2 small, v0 has three memory banks, at the residual stream after transformer blocks 4, 8 and 12. Code numbering calls these blocks 3, 7 and 11 because indexing starts at zero. Each key is obtained from the 768-number activation vector at the last input position, using a fixed centering and normalization formula. There is no separately trained semantic reader between that activation and the v0 key.

For each bank, v0 finds the nearest active stored key **within that slot's allowed radius**. If none qualifies, that bank adds zero. If one qualifies, its stored correction vector is added. The prediction then continues through the model with the correction applied.

Teaching a multi-token answer can create or modify slots for its successive answer prefixes, including the terminating newline. For example, after being taught a target of several tokens, the cap needs to support the first token, then the next token given the preceding target tokens, and eventually stopping. A v0 slot therefore is not necessarily one complete fact. Training uses the supplied answer prefixes; free generation at test time uses the tokens the model actually produces.

In this main study, stable v0 learned writes using ordinary adjoint/gradient credit and the v0 transactional search rule, with up to five rounds per answer prefix. The bank memories change during acquisition; the frozen base does not. [Sources 2 and 4.]

### Precisely what makes it “stable”

The original **live v0** computes a deeper bank's retrieval key after earlier banks have already changed the activations. Consequently, an early correction can change which memory a later bank recognizes.

**Stable v0 first runs the current input prefix through the base with no cap writes. It obtains all three retrieval keys from that write-free pass.** It then applies the banks' corrections in depth order, while continuing to use those previously obtained keys for retrieval. The same convention applies when learning a correction and when retrieving it later.

For the same input tokens and the same frozen base, the source activation for a stable key does not move just because another bank has made a correction. The output computation still incorporates the corrections: only the source of the retrieval keys is kept independent of them.

There are limits to this stability:

- A paraphrase changes the input tokens and can produce a different key.
- As generation proceeds, the prefix changes, so the next answer position gets new keys. An earlier generated mistake can change later prefixes.
- Subsequent learning can change the contents of the memory, including which slots exist and what values they hold. A stable key does not guarantee that its former correction remains available or wins retrieval.

Stable v0 addresses **retrieval keys moving because of upstream writes**. It does not solve semantic generalization or memory interference by itself. The newer learned-reader design also observes the write-free base, but uses a learned representation and a different memory organization. [Source 4.]

### A consequential setting in the actual runs

Stable v0's registered retrieval radii differed by dataset:

| Dataset | Radius at banks 1 / 2 / 3 | Practical meaning |
| --- | --- | --- |
| zsRE | Approximately 0.281 / 0.414 / 0.189 | Nearby activation keys can match. This allows some generalization, but also potential interference and unintended matches. |
| CounterFact | 0 / 0 / 0 | Effectively exact activation-key matching. |
| MQuAKE | 0 / 0 / 0 | Effectively exact activation-key matching. |

Zero radius includes a small numerical tolerance, `1e-4`, for floating-point differences. It is not a literal string-equality test, but it is much more restrictive than a semantic paraphrase matcher. These were pre-existing calibrated settings used in the final recipes, not radii selected after examining the final results.

This helps explain an otherwise puzzling result: on CounterFact and MQuAKE, stable v0 retained the taught original answers perfectly, yet had zero final paraphrase success. It could store a correction and recognize the original activation pattern without recognizing a differently worded request for the same fact.

On the ordinary-text validation inventory, those two stable-v0 groups also recorded zero KL and zero loss change. A restrictive retrieval rule can preserve ordinary text by rarely applying an edit there, while failing to apply a desired edit to a paraphrase. These results do not establish universal safety. zsRE's wider-radius stable v0 had both retention failures and measured ordinary-text harm. [Sources 1, 4 and 5.]

## How the other two caps differ

| Question | Learned reader v5 | Random-geometry reader + gate | Stable v0 |
| --- | --- | --- | --- |
| Was a reusable reader trained beforehand? | Yes, by backpropagation. | No; its reusable parameters came from a fixed random checkpoint. | No learned reader; fixed normalized activation keys. |
| Does it learn the supplied edits during the stream? | Yes. | Yes. “Random” does not mean its correction values are untrained. | Yes. “Stable” does not mean its memory is untrained. |
| How is memory selected? | Learned prompt representation, lexical features, learned null decision and an additional rare-token overlap gate. | Random representation with a fixed cosine-similarity threshold of 0.93. | Nearest qualifying slot in each bank's activation space. |
| How is a correction organized? | A fact record with per-answer-position correction vectors; the record is selected from the question and held for that answer. | The same general record/delta-write framework. | Bank slots associated with answer-prefix activation keys; retrieval occurs as generation proceeds. |
| What stays fixed while edits are acquired? | Base weights and reusable reader/controller weights. | Base weights and random reusable parameters. | Base weights and the key rule/configuration. |

For learned v5 and random geometry, the main run used up to five normalized adjoint updates per answer position to learn explicit **delta writes**. When a record has these deltas, they supply its activation correction in place of the controller-generated write. The repository also contains other adaptation options, but those were not the rule used for this comparison.

The selected learned checkpoint was the average of training steps 150, 200, 250 and 300 from **one** training run, `r1_50_stream_sel6_text_s2`, with training seed 2. Its selection manifest is dated September 15. That same selected checkpoint was reused across all 45 learned-reader cells. The random cells likewise reused one fixed random checkpoint. Each started its own correction memory.

The learned training run drew episodes from pools containing 1,000 CounterFact items, 1,000 zsRE items and 500 MQuAKE items, with internal development holdouts, 64-record training memories and examples on which the reader should abstain. This taught reusable behavior before the final streams; it was not a prefilled memory of their final edit sequences.

If “timing” means duration: this selected run's saved training-loop timer is about **17.2 minutes**. That is only one run's training loop. It excludes the broader search over candidates, previously constructed feature banks, all final per-edit learning and evaluation, and the later predictive-coding supplements. It should not be presented as the total cost of building or testing the cap. [Sources 2, 3 and 6.]

### A qualification to slide 10's wording

“The central comparison changes the reader” is a useful introduction, but it compresses several differences. Stable v0 versus learned v5 compares memory designs and acquisition procedures as well as retrieval. Even learned versus random is not a perfectly isolated “train exactly this same reader and change nothing else” test: the gates and lexical features differ too.

In particular, the older support README's phrase “the same gate” should not be read literally. The random condition disables the learned null threshold as a rejection rule (`null_threshold=1.01`), has no learned-reader lexical/pairwise-null features, and uses its cosine gate. The learned condition uses `null_threshold=0.5` and its rare-token gate. A precise spoken description is: **“We compared three ways of storing and retrieving corrections, using the same frozen base and paired edit streams.”**

## Where the no-cap transformer enters the comparisons

For these three conditions, **no cap**, **cap off**, and **original frozen base** refer to the same underlying GPT-2 prediction system. An attached cap with an empty memory also produces base predictions. Later, a cap that abstains completely for a prediction applies zero correction and gives the base result for the same input prefix.

There are two different questions in the experiment:

1. **On a fact we deliberately taught, does the cap produce the supplied target?** Here we want the requested new behavior.
2. **Away from the intended edit, does the cap preserve what the original model would do?** Here we usually want no change.

The score's reference therefore depends on which question is being asked.

| Measurement | What is compared? | Role of the uncapped model |
| --- | --- | --- |
| Immediate edit success, **ES** | The capped answer just after teaching versus the supplied target/accepted aliases. | It is not the answer key. The reported percentage is target accuracy, not percentage-point improvement over no cap. |
| Retained original-prompt success, **RET-ES** | The capped answer to an earlier teaching prompt, after subsequent edits, versus its target. | Same distinction. This tests whether the correction remains usable. |
| Retained paraphrase success, **RET-GS** | The capped answer to an alternative wording versus that fact's target. | Same distinction. Slide 11 shows absolute capped-system scores, not capped-minus-base differences. |
| Locality, **LS** | Capped generated text versus original-base generated text on reserved prompts. | It directly supplies the preservation reference. Preserving an incorrect or empty base answer still counts as preservation. |
| Near-miss preservation | After teaching a challenge fact, the answer to a related but different subject's prompt versus that neighbour's own cap-off answer. | It directly supplies the reference, rather than the neighbour's stored dataset answer. |
| Ordinary-text **KL** | The cap's next-token probability distribution versus the base's distribution at the same text prefix. | It directly supplies the distribution being preserved. The recorded direction is KL(base ∥ cap). |
| Ordinary-text **ΔNLL**, including harm tails | Loss on the actual next text token with the cap, minus loss without it. | It directly supplies the baseline loss. Positive means the cap made that observed token less likely. |
| Revision | Teach an earlier answer, then a newer answer, and test adoption of the newer one and reappearance of the earlier one. | The primary desired answer comes from the supplied revision, not from the original base. Record-retirement diagnostics apply to the newer record-based design; v0 has no equivalent declared record structure. |

The text-generation tests use a bounded greedy decoder, at most 32 new tokens, stopping on the configured newline/EOS. Edit success requires a complete accepted answer under the registered alias normalization and rejects truncation. Locality's primary rule is equality of the bounded decoded text; termination/truncation diagnostics are retained separately.

The ordinary-text tests supply the same recorded text prefix to both systems. They do not compare two freely generated passages that have already diverged. Consequently, the token-level harm measurements isolate how the cap changes probabilities given identical preceding text.

The principal tables do not provide a separate no-cap ES/RET-GS row. That does not mean the base was absent from the study: it is central to the preservation measurements. However, we should not invent an aggregate no-cap target score from those tables, assume it is always zero, or describe a capped accuracy as an experimentally reported gain over no cap.

In the human-readable examples here, the explicitly labelled base-alone edit/paraphrase answers were generated later on CPU for explanation. The capped answers were copied from the saved experimental results. Those additional illustrative base answers are not a newly registered aggregate endpoint. Because the base is frozen, it never accumulates the edit stream; a later no-cap query is not a secretly trained or updated model. [Sources 1, 3 and 7.]

## Two actual examples that make these distinctions visible

These are saved realization-0, order-100 examples, evaluated after 1,000 edits. Leading display spaces are omitted. They illustrate behavior; they are not a representative substitute for the complete result tables.

**James Howell, CounterFact:** the original prompt was “James Howell speaks”; the supplied new target was **Spanish**. The dataset's previously true answer was **English**. But the uncapped model actually continued the original prompt with a passage about speaking to the media after a sports game. It did not produce the dataset label “English.”

The tested paraphrase was “Cataraqui is also the name of a municipal electoral district. The language used by James Howell is”.

| System | Original prompt at end of stream | Paraphrase at end of stream |
| --- | --- | --- |
| No cap | Sports/media continuation, reaching the token limit | `"the city of the people."` |
| Learned reader | Spanish | Spanish |
| Random reader | Spanish | Ukrainian |
| Stable v0 | Spanish | `"the city of the people."` |

All three caps had successfully acquired Spanish immediately after teaching it. Stable v0 still produced Spanish from the original prompt at the end. Its paraphrase output equalled the uncapped output, which is consistent with its restrictive retrieval mechanism. The saved v0 example does not contain a firing trace, so matching text alone does not prove that every bank abstained.

Crucially, equality with the base on **this paraphrase** is a failure: it asks for the fact we meant to change. Equality with the base on an **unrelated locality prompt** would be a preservation success. Whether change is desirable depends on the prompt's experimental role.

**Sporting Canamy, zsRE:** the original question was “What league was Sporting Canamy?” and its supplied target was **Tercera División de México**. Its paraphrase was “What league did Sporting Canamy join with?” The base returned an empty answer, stopping on a newline, to both prompts.

| System | Immediately after teaching, original prompt | Final original prompt | Final paraphrase |
| --- | --- | --- | --- |
| Learned reader | Tercera División de México | Tercera División de México | Tercera División de México |
| Random reader | Tercera División de México | Tercera División de México | CD Atlético Baleares |
| Stable v0 | Tercera División de México | Empty answer | forward |

Here stable v0 did learn the target initially. Its later failure is therefore not evidence that it was never trained. It shows that the learned correction was no longer successfully expressed after the rest of the stream. The differing paraphrase output also shows that stable v0 need not simply reproduce the base on every unfamiliar wording. These saved answers alone do not diagnose the precise slot-level cause of the failure. [Source 7.]

## What the aggregate results say about stable v0

The following are final scores averaged over orders within each realization and then across the three realizations:

| Dataset | Stable v0: original-prompt retention | Stable v0: paraphrase retention | Learned reader: paraphrase retention |
| --- | --- | --- | --- |
| zsRE, 1,000 edits | 66.68% | 18.56% | 96.03% |
| CounterFact, 1,000 edits | 100% | 0% | 67.80% |
| MQuAKE, 300 edits | 100% | 0% | 71.56% |

These results distinguish **storage**, **retention**, and **finding the correction under a new wording**. They also reveal a tradeoff: the learned reader generalizes much better to paraphrases, but all 45 of its cells exceeded the registered mean-KL preservation benchmark of 0.001. Its CounterFact comparison against stable v0 received an inconclusive registered classification because a locality requirement failed, despite the large paraphrase advantage. MQuAKE's shorter run remains descriptive.

Stable v0 is therefore a substantive comparator. It demonstrates that excellent memory for the original prompt can coexist with little or no paraphrase generalization. It also gives a useful preservation reference, especially where narrow retrieval largely leaves ordinary text alone. [Source 1.]

## Two other uses of “base” and “v0” elsewhere in the deck

**Continued-base controls are separate from slide 10.** In the wider study, S1_LM first continued training the base on ordinary text and then froze it before attaching a stable cap. S1_literal used literal self-distillation from the original teacher, then a stable cap. Contrary to the older support README's wording, S1_literal was not ordinary fine-tuning on the final experiment's supplied new target answers. The U03 methods memo defines it as a numerical negative control whose identical teacher/student objective has zero gradient in exact arithmetic.

For an S1 system, there are consequently two distinct uncapped references: **its own continued base with the cap disabled**, and **the original GPT-2 base before continuation**. Cap versus own cap-off isolates the added cap's effect. Cap versus original base includes continuation as well. The full ordinary-text assays retain both; locality uses the original base, while near-miss preservation uses the system's own cap-off base. A very small cap-versus-own-base change does not prove that continuation left the original model unchanged. These S1 controls also do not constitute a direct baseline that fine-tunes GPT-2 on each final factual edit. [Sources 3 and 8.]

**The later predictive-coding results are separate experiments.** Slide 10's stable-v0 condition uses the 124M GPT-2 base and ordinary adjoint credit for its edit acquisition. The later corrected legacy PC-v0 experiments used a separately distilled ePC checkpoint and live C1 keys. That checkpoint also has 12 blocks and approximately 124M parameters; “50m” in its name refers to its distillation training-token budget, not its parameter count. The later reader BP-versus-ePC supplement trained additional reusable readers. Those readers did not retroactively supply the weights for the main slide-10 results. Neither the word “v0” nor the word “cap” by itself establishes that a particular experiment used predictive-coding credit. [Sources 1, 2 and 9; October 7 size clarification verified against the checkpoint in the new [architecture explanation](gpt2-blocks-cap-layers-and-distillation.md).]

## A short explanation to say aloud with slide 10

“All three systems start with the same pretrained transformer, whose weights we leave frozen. Each builds its own correction memory as we teach the edit stream. Stable v0 looks for stored activation patterns using a fixed rule. Its keys come from a clean pass through the base, before the cap's corrections can disturb those keys. The newer cap has a reader trained beforehand to recognize which correction applies; that reader then stays fixed while new corrections are stored. We test both whether the requested changes work and whether unrelated behavior remains close to the uncapped transformer.”

## Sources for checking the details

These links are local, so they open the exact materials used for this explanation.

1. [Complete Stage-4 triplet report](../../pc_cap/docs/R1_stage4_report_triplet.md) and [current full report](../../pc_cap/docs/R1_stage4_report.md): aggregate results, uncertainty and interpretation.
2. [Condition factory](../../pc_cap/src/pccap/revision_v1/stage4_adapters.py), [record-based learner](../../pc_cap/src/pccap/revision_v1/learner.py), [edit adaptation](../../pc_cap/src/pccap/revision_v1/adapt.py) and [controller](../../pc_cap/src/pccap/revision_v1/controller.py): fixed weights, gates, delta writes and query behavior.
3. [Actual stream driver](../../pc_cap/scripts/r1_68c_dev_cell.py), [checkpoint assays](../../pc_cap/src/pccap/revision_v1/stage4_assays.py), [challenge endpoints](../../pc_cap/src/pccap/revision_v1/endpoints.py) and [full ordinary-text validation](../../pc_cap/scripts/r1_68f_full_validation.py): teaching, scoring, restoration and reference systems.
4. [StableCap implementation](../../pc_cap/src/pccap/revision_v1/v0_stable.py), [original Cap](../../pc_cap/src/pccap/cap/cap.py), [key features](../../pc_cap/src/pccap/cap/features.py), [bank retrieval](../../pc_cap/src/pccap/cap/bank.py) and [v0 learning rule](../../pc_cap/src/pccap/cap/learn.py): exact meaning of stable keys and memory learning.
5. Final stable-v0 recipes for realization 0, order 100: [zsRE](../../pc_cap/docs/tasks/R1-final-cell-recipes/39c7fd4929721e8dcba56b94.json), [CounterFact](../../pc_cap/docs/tasks/R1-final-cell-recipes/baa601113af675024e73bc30.json), [MQuAKE](../../pc_cap/docs/tasks/R1-final-cell-recipes/c2f9d3102987f746f4f31b8d.json). All 135 triplet recipes were checked for shared base identity, per-condition reusable weights and dataset radii.
6. [Selected v5 manifest](../../pc_cap/manifests/revision_v1/primary_condition_v5.json), [selected-run training summary](../../pc_cap/results/R1/pilot/r1_50_stream_sel6_text_s2/summary.json), [learned final recipe](../../pc_cap/docs/tasks/R1-final-cell-recipes/61348508e40d54351613ab14.json) and [random final recipe](../../pc_cap/docs/tasks/R1-final-cell-recipes/f3dbf1a3d5860a628e7d68ef.json). The historical selection manifest predates the final freeze; the final recipes establish which checkpoint actually entered these runs.
7. [Saved example data](examples.json), [CounterFact examples](examples-counterfact.md), [zsRE examples](examples-zsre.md) and [example construction code](../../pc_cap/aw/support_examples.py): actual outputs and the later illustrative no-cap decoding.
8. [U03 continuation-control interpretation](../../pc_cap/docs/R1_U03_interpretation_memo.md): S1 training, its limitations and why own-cap-off and original-base references differ.
9. [Long-deck source](../presentation-materials/deck_v4/long_deck_v1.md): separation of the main study from corrected PC credit and subsequently trained-reader supplements.
