# MQuAKE: a single edited fact versus a chain of consequences

Prepared by Capex, 2026-10-09. Companion: [comparison of all three datasets](datasets-overview.md).

**MQuAKE's distinctive idea is to test whether an edited fact changes answers to questions that depend on several connected facts.** Our headline MQuAKE retention result, however, concerns **individual facts and their single-fact paraphrases**. A separate composition assay probes the connected-fact question. Keeping these two uses apart is essential.

## Which MQuAKE resource we used

The benchmark is introduced in **MQuAKE: Assessing Knowledge Editing in Language Models via Multi-Hop Questions**. Its official collection includes counterfactual edits, called MQuAKE-CF, and temporal updates, called MQuAKE-T. Our source is the full **MQuAKE-CF.json**, containing 9,218 cases. The downloaded temporal set and revised 3,000-case subset are reference resources, not the source of the main stream described here. [Official project](https://github.com/princeton-nlp/MQuAKE).

Counting the local full file gives **16,835 rewrite occurrences across those 9,218 cases**. A case can request multiple changes, and the same subject/relation can occur in several cases. Therefore cases, rewrite occurrences, and distinct editable facts are different counts.

The preparation code groups rewrites by normalized subject and relation ID, producing stable fact IDs. It selects the first representative in source case-ID order and records conflicting later targets. It does not silently turn conflicting replacements into additional simultaneously true memories.

After exclusions, checks, and reservations, the completed confirmatory streams contain **300 individual edits per realization**. They have three realizations and five orders each. The 300-edit endpoint is descriptive; it is not a measured 1,000-edit endpoint.

## The two levels of a source case

| Source field | Meaning |
| --- | --- |
| `requested_rewrite` | List of individual facts the case asks to change |
| A rewrite's `prompt` and `subject` | Template and entity for teaching one changed fact |
| A rewrite's `target_true` / `target_new` | Original and replacement answer for that one fact |
| A rewrite's `question` | Question form asking for that same individual fact |
| `single_hops` | Original one-step facts in the reasoning chain |
| `new_single_hops` | One-step facts in the changed chain |
| `questions` | Three alternative multi-hop questions about the chain |
| Top-level `answer` / `new_answer` | Original and replacement answer to the multi-hop question |
| `orig` | Underlying entity/relation chains before and after editing |

A **hop** is one link in a chain. Finding a person's institution is one hop; finding that institution's location adds another. A question about the location of a person's institution requires both.

The top-level `new_answer` is therefore not interchangeable with a rewrite's `target_new.str`. One may be a city, while the other is the name of an institution.

## Actual single-fact example: Marion Brown

Source case **7148** contributes item **`mquake:3218c8106c48e72c7297475f`** to the shown realization-0 stream.

| Use | Exact source text or label |
| --- | --- |
| Teaching prompt | The type of music that Marion Brown plays is |
| Original answer | jazz |
| Requested target | West Coast hip hop |
| Single-fact paraphrase | What type of music does Marion Brown play? |
| Additional accepted answer alias | West Coast rap |

This is a deliberate replacement. In this task, a correct edited answer is “West Coast hip hop” or an admitted alias, not a claim about Marion Brown's actual musical history.

The teaching input is a sentence stem; the paraphrase is a question. The reader must connect “The type of music that … plays is” with “What type of music does … play?” That changes grammatical form while preserving the requested relation.

The replacement was already in the source's `target_new.str`. Our preparation and evaluation did not randomly pick a new genre at teaching time or ask the model to propose one.

In the saved example, frozen GPT-2 continues the sentence with prose mentioning classical music and jazz, but answers the question form with empty text. The learned reader produces **West Coast hip hop** immediately after teaching, on the original prompt after 300 edits, and on the paraphrase after 300 edits. These are three distinct checks, all successful for this particular item. [Recorded examples](examples-mquake.md).

## How we assemble the single-fact paraphrases

The preparation starts with the selected rewrite's `question`. It can also collect question and cloze variants from other occurrences of the same subject/relation with the same replacement identity, plus matching entries in `single_hops` and `new_single_hops`.

Matching is constrained by the target and the question/cloze text. A question about a different hop is not made into a paraphrase merely because it occurs in the same source case. Repeated strings and the original teaching prompt are removed from the variants.

In the actual sealed main streams, **every edit has one retained single-fact paraphrase**. That is the denominator used for the headline MQuAKE RET-GS result. It is not three.

Answer aliases are gathered separately from matching `new_single_hops` records. For Marion Brown, **West Coast rap** is an answer alias. It is not an alternative question.

A second actual edit shows the distinction clearly:

| Use | Exact source text or label |
| --- | --- |
| Source case / item | 4080 / `mquake:347280026977b8d78c05f27b` |
| Teaching prompt | The origianl broadcaster of The Eddie Capra Mysteries is |
| Original answer | NBC |
| Requested target | CBS |
| Single-fact paraphrase | Who is the original broadcaster of The Eddie Capra Mysteries? |

The misspelling **origianl** is in the source template and is preserved in our experimental prompt. The question uses the correct spelling. Source aliases for CBS include **Columbia Broadcasting System**, among others.

A successful target match on this prompt tests the broadcaster fact. It does not establish that the model can use the broadcaster's other properties to answer a longer question.

## The three multi-hop paraphrases are another object

Return to Marion Brown's source case 7148. It requests **two** changes:

1. Marion Brown's genre: **jazz → West Coast hip hop**.
2. The United States' capital: **Washington, D.C. → Harrisville**.

These are instructions within a fictional edited world. In that world the source's changed chain is:

> Marion Brown → West Coast hip hop → United States of America → Harrisville

The relation labels are, respectively, genre, country of origin, and capital.

The case's three multi-hop questions are:

1. **What is the capital of the country where Marion Brown's music genre originated?**
2. **Which city serves as the capital of the country where Marion Brown's music genre is from?**
3. **What city is the capital of the country where the music genre associated with Marion Brown originated?**

The expected answer to these questions is **Harrisville**, not **West Coast hip hop**.

This is why the one single-fact paraphrase and the three multi-hop paraphrases cannot be pooled into one score. The first asks for a genre; the others ask for a city reached through a chain.

This source case illustrates the structure; it is **not** a claim that all of its dependencies were taught together or that it was an admitted composition test in the shown stream. The saved Marion Brown item reports zero available-dependency composition questions in its preparation metadata.

The official repository attributes the generation of its three multi-hop `questions` to GPT-3.5-turbo. That attribution applies to those chain questions; it should not be extended without evidence to every single-hop field. We reused the downloaded questions rather than generating new ones for our experiment. [Official data-format description](https://github.com/princeton-nlp/MQuAKE#data-format).

## A composition test that actually ran

The saved learned-reader checkpoint for **realization 0, order 100, checkpoint 300** contains a separate composition record for source case **179**. This gives a concrete example beyond the source's intended design.

The taught change is:

> Percival Lowell — educated at — Harvard University
>
> becomes
>
> Percival Lowell — educated at — Santa Monica College

The changed chain ends with:

> Percival Lowell → Santa Monica College → Santa Monica

The source's final target is the city **Santa Monica**. Its three questions are:

1. **What is the location of the headquarters of the institution where Percival Lowell was educated?**
2. **Where is the institution located, whose alumni include Percival Lowell?**
3. **Where is the headquarters of the institution where Percival Lowell received his education located?**

The recorded cap outputs are **Santa Monica College**, then empty text, then empty text. All three fail the city's accepted-answer test. Giving the institution's name instead of its location is a useful illustration of the difference between retrieving one edited association and answering the composed question. This interpretation describes the output; it does not establish the model's internal reasoning process.

The code runs this assay by restoring an independent declared teaching state, teaching the case's required edits, asking the three direct questions, and restoring the ongoing experiment's state afterward. It is an **isolated dependency-edit test**, not a measurement that the same multi-hop answer survived the entire accumulated stream.

Our local case-success rule requires **all three** question forms to produce an accepted new answer without truncation. The source project's documented rule accepts a case when **any** of its three questions succeeds. Our result therefore cannot be compared numerically with the source's published score as if the success definitions and model setup were identical.

For this one saved learned-reader checkpoint, its existing composition summary records:

| Quantity | Saved value |
| --- | --- |
| Planned and scored source cases | 80 |
| Cases satisfying our all-three success rule | 0 |
| Individual question forms matching the new answer | 2 of 240 |
| Scope | Secondary descriptive diagnostic |

These are copied checkpoint values, not a new pooled analysis and not a result for every condition or realization. They also do not prove that all possible approaches fail at composition.

There is a reporting distinction worth preserving: the assembled Stage-4 report lists composition as unavailable because the **upstream aggregate reporting adapter** was missing. Its native appendix states that reason explicitly. That should not be paraphrased as “no composition model calls were made.” Saved checkpoint-level measurements exist, as this example shows. [Native report appendix](https://github.com/pderp/pc_cap/blob/master/logs/R1/reports/comparators-270/appendix/report.md).

## Locality and near misses use other subjects

MQuAKE does not provide precisely the same neighbourhood list as CounterFact. Our preparation constructs candidate neighbours from other subjects sharing the source relation. Final assay reservation is separate from those per-item candidate lists.

For example, one actual near-miss case teaches:

> Lorenzo Valla is affiliated with the religion of → **Methodism**

and then checks:

> Jean-Luc Dehaene is affiliated with the religion of

The second subject should retain its own cap-off response. The test does not ask whether both people happen to share a source label or whether the first target can be emitted for both names.

The final ordinary-locality inventory also has 50 prompts. One is “Marten Stekelenburg plays the position of.” Again, preservation is exact agreement with the reference model's bounded response, not verification of a sporting fact.

The preparation retains awkward source statements, including template/type mismatches. For example, the existing stream includes “Keio University is a citizen of.” That is a warning about interpreting the benchmark's linguistic quality, not something generated by our cap. The answers and queries remain traceable rather than silently rewritten into a cleaner task.

## What MQuAKE contributes to our evidence

The single-fact stream tests whether a learned retrieval mechanism can carry requested replacements from statements into question forms. It provides a different source population and linguistic pattern from zsRE and CounterFact.

Its multi-hop structure additionally lets us ask whether retrieval of individual edits supports their consequences. The recorded Percival Lowell example shows why that question needs its own assay: success at retrieving the edited institution does not amount to answering the institution's city.

The published learned-reader main-stream RET-GS mean is **0.71556 at 300 edits**. It is a single-fact paraphrase-retention result. It must not be called 71.6% multi-hop reasoning accuracy. MQuAKE ran only the learned-reader, random-reader, and stable-v0 triplet in this main study, with the longer endpoint and additional comparators unavailable. [Stage-4 report](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report.md).

## Exact sources for checking these explanations

- [Raw full MQuAKE-CF download](../data/raw/mquake/MQuAKE-CF.json): cases 7148, 4080, and 179.
- [Pinned downloaded README](../data/raw/mquake/README.md).
- [Preparation and provenance logic](https://github.com/pderp/pc_cap/blob/master/scripts/r1_d4_prepare_mquake.py).
- [Composition evaluator and all-three success rule](https://github.com/pderp/pc_cap/blob/master/src/pccap/revision_v1/endpoints_composition.py).
- [Worked single-fact examples](examples-mquake.md), [random examples](examples-mquake-random.md), and [examples.json](examples.json).
- Local checkpoint: `pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/checkpoint-300.json`, under `endpoints.composition`. The single case is identified by `composition_id: mquake:case:179`.

The raw-file SHA256 is `fbf1ab9e5243e52da429f7636990096ae0b5f8fbf60f1d4d3a4bf0c9214cd6ea`. The checked example payload SHA256 is `b1e583b366456d0a7b8b83ba504d8878254057f24ca33b660011df6589a4b5d7`. The learned-reader checkpoint SHA256 is `0746efdcf687d2c125b63e3d5007e13720c6ead66694571fb694f7b9f0286988`.
