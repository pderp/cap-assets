# zsRE: learning an answer and recognizing the question again

Prepared by Capex, 2026-10-09. Companion: [comparison of all three datasets](datasets-overview.md).

**In our experiment, zsRE asks whether the cap can acquire a factual answer, retain it while other facts arrive, and retrieve it when the question is reworded.** Our main stream teaches the dataset's reference answer. It does not replace that answer with the source file's alternative `alt` value.

## Where zsRE comes from

zsRE stands for **zero-shot relation extraction**. A relation connects a subject to some information about it: a person to a birthplace, a musician to a genre, or a footballer to a position. The original work expressed relation extraction as answering natural-language questions about text, including relations absent from training. That is the origin of “zero-shot”; it is not a claim that our cap or reader received no training. [Levy, Seo, Choi and Zettlemoyer, 2017](https://aclanthology.org/K17-1034/).

Our immediate source is the editing-format dataset distributed through ROME, specifically `zsre_mend_train.json` for the confirmation examples discussed here. The local download contains **163,196 source records**. It is an upstream collection, not the number of edits we ran.

The project also downloaded `zsre_mend_eval.json` and used it in early work. The `zsre-train-...` IDs in the current example collection identify the later train-file source unambiguously. Our confirmation streams contain 1,000 selected facts per realization, after our own exclusions and eligibility checks.

## What a record looks like

This is the actual source record at zero-based row **14871**, mapped to item **`zsre-train-14871`**:

| Source field | Saved value | Role in our experiment |
| --- | --- | --- |
| `subject` | Sporting Canamy | Entity the question concerns |
| `src` | What league was Sporting Canamy? | Teaching prompt |
| `answers[0]` | Tercera División de México | Target answer |
| `rephrase` | What league did Sporting Canamy join with? | Held-out alternative prompt |
| `alt` | Segunda División B | Supplied alternative; not our main-stream target |
| `pred` | Primera B Metropolitana | Upstream stored prediction; not our GPT-2 measurement |
| `loc` | nq question: who played the original roman on days of our lives | Unrelated source prompt |
| `loc_ans` | Wayne Northrop | Source answer associated with that unrelated prompt |

The source also has a `cond` string connecting its stored prediction, alternative answer, and question. That upstream editing instruction is not what determines our target. Our mapping explicitly takes the first `answers` entry and keeps the other reference answers as accepted aliases.

Thus, for this actual experiment, the requested behaviour is:

> “What league was Sporting Canamy?” → **Tercera División de México**

and, when tested differently:

> “What league did Sporting Canamy join with?” → **Tercera División de México**

The league name comes directly from the dataset. We did not draw a random replacement league for this run. Randomly selecting eligible items or rearranging their order is different from randomly choosing their answers.

## What the paraphrase changes

The two questions keep the same subject and ask about its league, but alter the syntax: “was” becomes “did … join with.” The intended answer stays fixed.

Another actual item, **`zsre-train-8237`**, is easier to read:

| Use | Exact text |
| --- | --- |
| Teaching prompt | What was the date of death of Fernando Mencherini? |
| Paraphrase | What was the date of Fernando Mencherini's death? |
| Target | 1997 |

The second question changes a “date of death of” phrase into a possessive construction. It is a test of whether the retrieval mechanism treats different word sequences as referring to the same stored fact.

A source-quality caveat is visible in **`zsre-train-2768`**:

| Use | Exact text |
| --- | --- |
| Teaching prompt | Who created Carnets de Géologie? |
| Supplied paraphrase | Who combined Carnets de Géologie? |
| Target | Bruno Granier |

“Created” and “combined” are not reliably interchangeable. We retained the source wording; it was not invented for the presentation or silently repaired afterward. This example shows why a benchmark paraphrase is an **intended** equivalent question, not a guarantee of perfect semantics.

The relevant experimental fact is that our preparation code copies the existing `rephrase` field. It does not ask a model to invent a new paraphrase during acquisition or testing. These guides do not claim that every upstream alternative was human-written or individually checked by a human.

## One alternative per item, tested after teaching

Each zsRE edit in the saved Stage-4 streams has **one** paraphrase. Therefore its generalization score at a checkpoint is either a successful answer to that alternative or a failure.

For the Sporting Canamy item, the saved realization-0, order-100 example shows:

| Observation | Recorded output |
| --- | --- |
| Frozen GPT-2 on the teaching prompt | Empty text; stopped immediately at newline |
| Frozen GPT-2 on the paraphrase | Empty text; stopped immediately at newline |
| Learned reader immediately after teaching | Tercera División de México |
| Learned reader after 1,000 edits, teaching prompt | Tercera División de México |
| Learned reader after 1,000 edits, paraphrase | Tercera División de México |

The saved cap outputs include a leading space, which normalization ignores. This is one observed success, not the overall performance estimate. It demonstrates the distinction between learning to answer the teaching question and recognizing its rephrasing later. The full tables include controls that can succeed immediately yet lose the answer or retrieve another fact later. [Recorded examples](examples-zsre.md).

## Why the base model's empty answers matter

The source characterization found that **6,036 of 6,084 eligible zsRE items** met the base-failure rule because the pinned GPT-2 emitted a newline immediately. That is a count for the characterized eligible population, not a claim that every sampled prompt or every possible zsRE question yields an empty answer. [Protocol's teacher-baseline limitation](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_protocol_v5_2_D_1.md).

GPT-2 is generating a continuation of a question under our fixed decoding rule. Its failure to produce the accepted answer is the criterion used here; we do not get to conclude that it first held a strong, explicitly stated false belief.

Accordingly, a careful description of much of our zsRE result is **answer acquisition and generalization from a largely empty response baseline**. Calling every case “correcting a fact GPT-2 used to answer incorrectly” would overstate what was observed. Teaching the reference answer can still be useful; the distinction changes the scientific interpretation.

The upstream `pred` field does not solve this problem. It is not a fresh output from the pinned GPT-2 in our experiment. For Sporting Canamy, that field says “Primera B Metropolitana,” while our measured base output is empty.

## Locality, near misses, and revision

The `loc` field provides a different question, often with the literal prefix `nq question:`. We preserve that prefix. These unrelated questions ask whether adding memory changes responses outside the taught facts.

Our final locality endpoint uses **50 distinct reserved prompts**, selected from eligible outside items' locality material and excluding collisions with reserved edit/paraphrase prompts. It does not mean we score the `loc` question attached to every one of the 1,000 stream items. For example, the first realization-0 locality prompt is:

> nq question: what is the name of fred flintstones wife

Preservation compares the cap's bounded response with the reference base's response, rather than scoring whether it knows the source answer.

The near-miss endpoint asks a more targeted question: can the cap distinguish two subjects in the same question pattern? A saved case teaches:

> Where was Frits Poelman from? → **New Zealand**

and then checks:

> Where was George Pitt Morison from?

Replacing each subject with a placeholder yields “Where was {subject} from?” The challenge is to avoid transferring the first person's stored answer to the second. The preservation reference is the neighbour's measured cap-off response, even when that response is empty. It is not a search for the most semantically similar entity in an embedding space.

There is also a separate two-version revision assay. For example, a reserved Tembenchi River question is first taught **Ider River** and later **Kochechum River**. This deliberately constructed revision challenge must not be confused with the main zsRE stream's policy of teaching `answers[0]`. The later target is supposed to replace the earlier one for that fact.

## What zsRE contributes, and what it cannot establish alone

It is a useful test of whether a learned reader can connect two question forms to one memory and keep doing so as memory grows. The common wording patterns also expose whether a system relies too heavily on relation words while ignoring the subject.

However, a high score is not evidence of arbitrary language understanding, reasoning across several facts, or successful correction of strongly held prior answers. Each fact has only one supplied alternative question. Some alternatives are close syntactic variants, and some are imperfect.

The published main-study learned-reader RET-GS mean is **0.96033 at 1,000 edits**, pooled as specified across realization and order summaries. That value describes the supplied test questions; it should be read alongside specificity and ordinary-text harm measurements. [Stage-4 report](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report.md).

## Exact sources for checking these explanations

- [Raw zsRE train download](../data/raw/zsre/zsre_mend_train.json): rows 14871, 8237, and 2768.
- [Candidate mapping](https://github.com/pderp/pc_cap/blob/master/scripts/r1_d1c_candidates.py): `map_item` explicitly defines the target and paraphrase policy.
- [Earlier loader and field convention](https://github.com/pderp/pc_cap/blob/master/src/pccap/data/splits.py).
- [Worked examples](examples-zsre.md) and [randomly selected examples](examples-zsre-random.md).
- [examples.json](examples.json): its `zsre.sources_sha256` identifies the realization-0/order-100 payload and checkpoint used above.
- [Near-miss family definition](https://github.com/pderp/pc_cap/blob/master/scripts/r1_d9e_near_family.py) and [scoring code](https://github.com/pderp/pc_cap/blob/master/src/pccap/revision_v1/stage4_assays.py).

The source train-file SHA256 is `4f3ac245e9c0baaf633f9e6cb765ffa8e83d594a74520a6cc3539497328c0722`. The checked example payload SHA256 is `66a3c7d79210dbfc50d642474d0c084da9cdd8b64141230038138e18971ccc7e`.
