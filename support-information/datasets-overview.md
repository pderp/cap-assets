# Our three editing datasets: what they test and how to read the examples

Prepared by Capex for charlie, 2026-10-09. This guide describes the data and measurements used in the completed Stage-4 experiment. The linked dataset guides trace examples from the downloaded source, through the experiment's saved inputs, to recorded outputs. No new model runs were performed for these explanations.

**zsRE tests answering a factual question under another wording; CounterFact tests adopting a requested replacement under different wording and context; our main MQuAKE stream tests single-fact replacements across sentence and question forms.** MQuAKE also contains a separate structure for asking whether changes propagate through a chain of facts.

Read the individual guides for the details:

- [zsRE: questions, reference answers, and rephrased questions](dataset-zsre.md).
- [CounterFact: deliberate replacements, contextual paraphrases, and neighbours](dataset-counterfact.md).
- [MQuAKE: individual edits and the separate multi-hop question structure](dataset-mquake.md).

## What a single editing task contains

A **prompt** is text we give the model. A **target** is the answer we want it to produce. A **paraphrase** is another input intended to ask for that same answer. An **alias** is another accepted spelling or name for the answer. A paraphrase changes the question; an alias changes the acceptable answer text.

For example, an actual MQuAKE item teaches the completion:

> The type of music that Marion Brown plays is → West Coast hip hop

Its single-fact paraphrase is:

> What type of music does Marion Brown play?

An accepted answer alias is **West Coast rap**. The source's original answer is **jazz**. The replacement is deliberately counterfactual: a successful experimental response follows the requested replacement, even when that replacement is not a true statement about the world.

Our zsRE stream differs: it uses the source's reference answer, rather than its supplied alternative answer. Consequently, “new target” does not mean “invented replacement” in all three datasets.

**None of these supplied labels proves what GPT-2 previously knew.** The original answer in a dataset, the requested target, and the frozen model's observed answer are three different things. The existing example files show actual no-cap outputs separately.

## The structural differences at a glance

The counts below describe each completed Stage-4 stream. There are three sampled realizations per dataset and five orderings of each realization's facts.

| Feature | zsRE | CounterFact | MQuAKE in our main stream |
| --- | --- | --- | --- |
| Main input form | A factual question | An unfinished factual statement | An unfinished factual statement |
| Target used | First source reference answer | Source's requested replacement | Source's requested replacement |
| Typical held-out input | Reworded question | Different statement template, often with an unrelated prefix | Question form of the taught statement |
| Scored single-fact paraphrases per edit | 1 | 2 | 1 |
| Edits per stream | 1,000 | 1,000 | 300 |
| Checkpoints | 100, 300, 1,000 edits | 100, 300, 1,000 edits | 100, 300 edits |
| Additional source structure | An unrelated locality question and answer | Neighbour, attribute, and generation prompts | Linked original/edited fact chains and three multi-hop questions per source case |
| Main interpretive limitation | Often acquisition from an empty base response | Rephrasing and distracting context change together | Single-fact retention does not establish multi-hop reasoning |

The paraphrase counts were checked against all 45 item-bearing saved payloads in the final seal directory, rather than inferred from the example viewer. The viewer displays only the **first** paraphrase. For CounterFact that hides the second test; the [CounterFact guide](dataset-counterfact.md) shows an actual item that passes the first and fails the second.

“Three realizations and five orders” does not mean fifteen unrelated sets of facts: the five orders reuse the same facts within a realization. An order tests sensitivity to the sequence in which facts are taught.

## What happens during an experiment

The learned reader is trained before the confirmatory streams, using separate development/training material. Training includes examples of original prompts, paraphrases, and queries for which no stored record should apply. This teaches a retrieval rule: when should a different-looking prompt use the same memory?

During a confirmatory stream, the system receives each new item's **teaching prompt and target** and adds or adjusts the corresponding memory. Later it is queried with the item's original prompt and its saved paraphrases. Those confirmation paraphrases test the taught fact; they are not extra teaching prompts for that fact's acquisition update.

This distinction matters. “Held-out paraphrase” means the particular confirmation fact's alternative wording was reserved for testing. It does not mean that the reader has never seen any paraphrase training, any similar relation, or any similar template.

The upstream filename `zsre_mend_train.json` is also not a statement about our experimental roles. Our own reservation procedure separates reader-training, development, and confirmation populations within the resources we use.

## What each measurement asks

| Measurement | Plain-language question | What counts |
| --- | --- | --- |
| Immediate edit success, ES | Can the system give the target just after this fact is taught? | Correct complete answer on the teaching prompt |
| Retained own-prompt success, RET-ES | Can it still answer the original prompt after later facts were added? | Correct complete answer at a checkpoint |
| Retained paraphrase success, RET-GS | Can it still use the fact when the question is worded differently? | Fraction of that item's paraphrases answered correctly, averaged over items |
| Locality, LS | Did an unrelated prompt's response stay the same? | Exact agreement with the bounded text generated by the reference base |
| Near-miss preservation | Did teaching one fact disturb another subject with the same relation or question template? | Preservation of the neighbour's cap-off response |
| Unseen-query behaviour | Does the memory intervene for a fact that was never taught? | Separate retrieval/false-fire diagnostics |
| Revision | Can a later version supersede an earlier value for the same fact? | A separate two-version challenge, with its own record and answer checks |
| MQuAKE composition | Can taught changes be used in a question requiring connected facts? | Separate direct-question composition assay; not RET-GS |

The saved realization-0 payloads reserve 50 locality prompts, 100 near-miss cases, 100 unseen items, and 50 revision cases per dataset. These are distinct inventories, not extra paraphrases of every edit.

A locality success means **unchanged**, not necessarily **factually correct**. If the base gives an empty or incorrect answer and the cap leaves it unchanged, that can pass preservation. Conversely, an accidental correction of an unrelated answer can fail preservation. These tests measure interference with an existing model, not general knowledge accuracy.

## How answers are scored

The model generates greedily: at each step it chooses the highest-scoring next token. A token is a piece of text, so 32 tokens does not necessarily mean 32 words. Generation stops at a newline or end-of-sequence token, with a maximum of 32 new tokens.

For Stage-4 edit and paraphrase success, the complete generated answer must match an allowed alias after Unicode normalization, case folding, trimming, and collapsing whitespace. The Stage-4 assay additionally rejects a generation that reached the limit without terminating.

The scorer does not use an LLM to judge whether a response “basically means the same thing.” It does not generally strip punctuation, articles, explanations, or extra sentences. **Spanish**, **spanish**, and a leading-space version can match the same alias; **Spanish, I believe** does not match an alias containing only **Spanish**.

With two CounterFact paraphrases, an item can score 0, 0.5, or 1 for generalization. With one zsRE or main-stream MQuAKE paraphrase, an item's score is 0 or 1. The main metric averages these item scores. MQuAKE's separate composition test has a different denominator and success rule.

## What the three datasets collectively tell us

They put different pressures on the same memory system: recognizing reworded questions, ignoring distracting context, transferring between statement and question forms, keeping facts available as memory grows, and avoiding applying a stored answer to the wrong subject.

The published Stage-4 learned-reader final RET-GS means are approximately **96.0% for zsRE, 67.8% for CounterFact, and 71.6% for MQuAKE**. The first two are measured after 1,000 edits; the last is descriptive at 300. These are the report's main-study values, not new estimates or a summary of every later supplemental experiment. [Stage-4 report](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report.md).

Those percentages do not by themselves rank the datasets' intrinsic difficulty. Prompt format, aliases, source selection, baseline behaviour, contextual distractions, and stream length differ. Nor is a high paraphrase score proof of broad reasoning: it establishes success on the supplied alternatives.

The datasets also do not directly measure heavy-tailed damage on ordinary prose. That part of the project compares token probabilities and losses on a separate WikiText-103 validation sample. A system can answer these edit prompts well while changing a small number of unrelated token probabilities severely. Likewise, predictive coding versus backpropagation is an algorithm comparison made using tasks; the dataset names alone say nothing about which learning algorithm produced a result.

## Source trail and scope

The explanations were checked against:

- [Download manifest](https://github.com/pderp/pc_cap/blob/master/manifests/datasets.json), the downloaded JSON files, and the field-mapping code linked in each guide.
- [Existing worked examples](Capstan-README.md), [machine-readable examples](examples.json), and the exact sealed payloads and checkpoints listed there with SHA256 hashes.
- [Stage-4 assays](https://github.com/pderp/pc_cap/blob/master/src/pccap/revision_v1/stage4_assays.py), [decoder](https://github.com/pderp/pc_cap/blob/master/src/pccap/data/decode.py), and [answer normalization](https://github.com/pderp/pc_cap/blob/master/src/pccap/metrics/editing.py).
- [Stream-reader training](https://github.com/pderp/pc_cap/blob/master/src/pccap/revision_v1/stream_train.py) and the [assembled Stage-4 report](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report.md).

Examples are identified by saved item or source-case IDs. They illustrate structure and recorded behaviour; they are not a newly sampled estimate of performance. The [random example collection](README-random-sample.md) complements the first-30 collection, whose items are the oldest memories by the end of a stream.
