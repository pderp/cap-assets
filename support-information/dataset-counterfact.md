# CounterFact: replacing a fact across wording and context

Prepared by Capex, 2026-10-09. Companion: [comparison of all three datasets](datasets-overview.md).

**CounterFact asks whether a requested factual replacement is specific enough to change the intended answer, general enough to work under other wordings, and restrained enough to leave other subjects alone.** It is explicitly counterfactual: the desired answer may intentionally contradict the source's original fact.

Our downloaded `counterfact.json` contains **21,919 cases**. Our Stage-4 streams use 1,000 selected edits per realization, with three realizations and five orders each.

## Origin and the idea of a fact triple

CounterFact was introduced with Meng and colleagues' **Locating and Editing Factual Associations in GPT**, the ROME paper. ROME is an editing method; CounterFact is its associated dataset. Using CounterFact does not mean our experiment runs the ROME editing algorithm. [Original project](https://rome.baulab.info/).

The source represents a fact using a **subject, relation, and answer**. In ordinary language, this might mean “this person — speaks this language — English.” It supplies both an original answer and a replacement, plus different prompts for testing the replacement and its specificity.

The original construction uses relation templates from ParaRel. Its replacement objects are sampled upstream from objects associated with the same relation, using a weighted sampling procedure; two alternative templates are selected for paraphrase tests. Our experiments consume the resulting saved records rather than resampling replacement answers. [ROME paper, Appendix D](https://arxiv.org/pdf/2202.05262).

## An actual case: James Howell

Source case **9366**, experiment item **`cf-9366`**, contains:

| Source field | Saved value | Meaning |
| --- | --- | --- |
| `requested_rewrite.subject` | James Howell | Subject |
| `requested_rewrite.relation_id` | P1412 | Source identifier for the language relation |
| `requested_rewrite.prompt` | {} speaks | Template with a subject slot |
| `target_true.str` | English | Original answer recorded by the dataset |
| `target_new.str` | Spanish | Requested replacement |

Filling the slot gives:

> James Howell speaks → **Spanish**

The replacement comes from `target_new.str`. Our script did not invent “Spanish,” select it after examining the cap's results, or choose a fresh language each time this question was asked.

The original label **English** is not proof that our frozen GPT-2 answered “English” on that prompt. In the measured no-cap example, GPT-2 instead continued with prose about speaking to the media after a sporting event. That output illustrates why a source fact and a model's actual answer need separate labels.

Nor is the cap being asked to decide whether the replacement is historically true. A success means following the controlled replacement instruction.

## What the two paraphrases actually look like

This same source case supplies **two** alternatives, copied unchanged into our saved experimental input:

1. **Cataraqui is also the name of a municipal electoral district. The language used by James Howell is**
2. **Thomasia discolor Steud. James Howell writes in**

Both are scored against **Spanish**.

The main prompt and both alternatives are unfinished statements, sometimes called **cloze prompts**. The model supplies the missing continuation. A paraphrase therefore need not end with a question mark.

The relation-bearing part changes from “speaks” to “The language used by … is” or “writes in.” The subject stays James Howell and the requested answer stays Spanish.

There is an additional change: unrelated text precedes the fact question. The Cataraqui sentence and the botanical-looking “Thomasia discolor Steud.” fragment were already in the downloaded source. We did not add them for our talk or introduce a new fact about James Howell with them.

These inputs test more than a simple synonym swap. The memory must identify the relevant subject and relation despite an altered context. The result combines sensitivity to wording with sensitivity to prefix distraction; our experiment does not isolate those two effects in this item.

A second real case, **`cf-9706`**, makes the same structure visible:

| Use | Exact text or label |
| --- | --- |
| Teaching prompt | The headquarter of Skinner & Eddy is located in |
| Original answer | Seattle |
| Requested target | Boston |
| Paraphrase 1 | They soon met with twelve club-wielding police officers. The headquarters of Skinner & Eddy is in |
| Paraphrase 2 | III'. Skinner & Eddy is based in |

The source's grammar and prefix fragments are preserved. These examples show what the system actually received, rather than polished reconstructions of the intended task.

## Why showing only the first paraphrase can mislead

Our existing example viewer prints the first alternative for readability. The actual Stage-4 retention assay tests **both**.

For James Howell, the learned reader's saved realization-0, order-100, checkpoint-1,000 record contains:

| Test | Recorded behaviour | Score |
| --- | --- | --- |
| Teaching prompt immediately after acquisition | Spanish | Success |
| Teaching prompt after the full stream | Spanish | Success |
| First paraphrase after the full stream | Spanish | Success |
| Second paraphrase after the full stream | A prose continuation beginning “his book, The Art of the Stealer…” | Failure |

The item's saved generalization score is therefore **0.5**, even though the first-paraphrase column in the short example page has a check mark.

The calculation is simply:

> 1 successful alternative ÷ 2 alternatives = 0.5

An item can contribute 0, 0.5, or 1 to RET-GS. The overall endpoint averages these item scores. Two alternatives do not become two independent experimental replications; they are related tests of the same taught fact.

This is also why the counts in a 30-item example page must not be substituted for the report's main endpoint.

## The surrounding prompts are different kinds of tests

CounterFact has several prompt collections. They are not interchangeable.

| Source collection | What it contains | How to interpret it here |
| --- | --- | --- |
| `paraphrase_prompts` | Other ways to ask for the edited subject's relation | Should return the replacement |
| `neighborhood_prompts` | Related prompts about other subjects | Useful material for checking that unrelated facts do not change |
| `attribute_prompts` | A separate collection of other-subject prompts associated with the relation | Not the two scored paraphrases |
| `generation_prompts` | Broader continuation stems about the edited subject | Not the two scored paraphrases and not our headline RET-GS endpoint |

For James Howell, source neighbourhood prompts include:

> The language used by Walt Disney is
>
> Steven Spielberg writes in
>
> James Clerk Maxwell speaks

Those are not paraphrases of the James Howell question: **the subject has changed**. Teaching that James Howell should answer “Spanish” should not make every language question return “Spanish.”

The source also supplies broader generation stems such as “James Howell was born in” and “James Howell's friends all speak the language of.” Their presence in the download does not mean we reproduced every original CounterFact evaluation. Our operational measures are the particular assays in the project.

## Our locality and near-miss assays

The final stream uses a separate reserved set of **50 locality prompts**, selected from outside items' locality material after collision exclusion. For realization 0, the first saved locality prompt is “route 16 can be found in.” The assay compares bounded generated text with the original reference base.

Thus the ten neighbourhood strings attached to the James Howell source row illustrate the source structure; they are not a claim that all ten were final locality measurements for that edit.

The **100 near-miss cases** are another inventory. Here, supports and neighbours must have different subjects and the same nonempty relation ID. A saved pair is:

> Daiki Arioka's profession is an → **politician**

with the neighbour:

> The occupation of Gustave Le Gray is

The wording differs, but both belong to the occupation relation. The question is whether teaching the support fact changes the neighbour's cap-off answer. We do not teach the neighbour simply because it has a stored source target, and we do not declare preservation by checking that target. Its actual base response is the reference.

This is a relation-family specificity test. “Near miss” does not mean the pair was chosen as the nearest pair in a learned semantic space.

## What CounterFact helps reveal

An exact-prompt lookup can appear successful immediately after teaching yet fail when the same relation is expressed differently. Conversely, a broad retrieval rule can generalize to the paraphrases but also apply the answer to unrelated subjects.

CounterFact therefore makes the tradeoff between **finding the right memory** and **declining the wrong memory** particularly visible. The contextual prefixes also test whether the representation can focus on the intended request.

The published learned-reader final RET-GS mean is **0.67800 at 1,000 edits**. The stable-v0 paraphrase mean is zero in the reported main comparison, but that does not mean stable v0 cannot store the exact teaching prompts. Its limitation here is transfer to the supplied paraphrases. The learned reader also has locality failures, so better paraphrase retention is not an unconditional win on every endpoint. [Stage-4 report](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report.md).

The study uses an approved CounterFact source exception: an item's membership in an older eligible pool did not alone count as prior exposure. Training selections and other exclusion reasons remained excluded. It would be inaccurate to claim a completely new, independently sourced benchmark or to infer that prior reader training contained these exact confirmation facts. The limitation is recorded as DEC-042 in the [decision register](https://github.com/pderp/pc_cap/blob/master/docs/decisions.md).

## Exact sources for checking these explanations

- [Raw CounterFact download](../data/raw/counterfact/counterfact.json): cases 9366 and 9706.
- [CounterFact field mapping](https://github.com/pderp/pc_cap/blob/master/src/pccap/data/splits.py), function `counterfact_item`.
- [Worked examples](examples-counterfact.md) and [randomly selected examples](examples-counterfact-random.md).
- [examples.json](examples.json): `counterfact.sources_sha256` identifies the sealed payload and the learned-reader checkpoint used above.
- [Stage-4 retention assay](https://github.com/pderp/pc_cap/blob/master/src/pccap/revision_v1/stage4_assays.py): evaluates every entry in `item.paraphrases`.
- [Example viewer](https://github.com/pderp/pc_cap/blob/master/aw/support_examples.py): deliberately displays only the first paraphrase.

The raw-file SHA256 is `d017056125178a13728594e66a801357a8db9ed7973a7425554bb4271de9fc6f`. The checked example payload SHA256 is `8e9c7bca19f622f0a1a88938863cd53e102be633805d951284ac832bce834ac1`. The checkpoint's `retention.rows` entry for `cf-9366` records `gs: 0.5`.
