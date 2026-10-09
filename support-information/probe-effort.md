# With the cap and without it: direct evidence and worked probes

Prepared by Capex for charlie, 2026-10-09.

**Yes. We have direct comparisons of frozen GPT-2 running without a cap and the same base running with a cap.** They show that a cap can make the requested answers available and sometimes generalize them to other wordings. They also show failures to generalize, unwanted answers on untaught prompts, and changes to ordinary-text probabilities.

This document gives **30 editing examples, each with an original prompt and a paraphrase: 60 explicit prompt comparisons**. It then adds **14 comparisons** covering unchanged responses, interference, and multi-hop questions. The answers below are copied from saved artifacts; no model was run to prepare this document. New arithmetic is limited to descriptive counts of those existing records.

## What exactly is being compared?

- **No cap:** the frozen, pretrained GPT-2 small, with no stored corrections applied.
- **Learned cap:** that same frozen base plus the main Stage-4 learned reader, `R1_learned_ff`, with the experiment's learned correction memory.
- **Stable v0 cap:** that same frozen base plus the earlier `v0_stable` cap and its memory.

The two capped systems have been taught the stream's requested answers; the unmodified base has not. This is a comparison of the resulting systems' behaviour, not an equal-information comparison against a base given the same facts in its prompt, or against a model fine-tuned on those facts.

The learned reader in this main study was trained using backpropagation. These examples establish what that capped system did; they do not by themselves establish a benefit from predictive coding. Continued-base controls, whose underlying model weights differ, are omitted from the direct three-way tables to keep the underlying GPT-2 comparison clear.

For zsRE and CounterFact, capped answers are taken **after 1,000 edits**; for MQuAKE, **after 300 edits**. Most examples use realization 0, order 100. Two additional CounterFact locality failures are explicitly marked as realization 2.

## Where the no-cap answers come from

There are three complementary forms of evidence:

| Evidence | No-cap answer provenance | Capped answer provenance |
| --- | --- | --- |
| Original editing prompts and first paraphrases | Saved CPU-only decodes produced for the October 4 support examples, using the pinned Stage-4 base | Saved final-checkpoint generations from the experiment |
| Locality, near-miss, unseen, and composition probes | Cap-off reference generations recorded inside the experiment's checkpoint | Matching cap-on generations from the same assay |
| Ordinary-text fidelity | Reference token distributions and losses | Cap-on distributions and losses at the same text positions |

The first row is an **after-the-run baseline replay**, not a claim that every displayed no-cap editing answer was recorded during the original GPU run. The [example builder](../../pc_cap/aw/support_examples.py) records that distinction and uses the same pinned base, greedy decoding, and 32-token stopping convention. CounterFact's stored teacher outputs also provide an earlier cross-check on original prompts.

The original answer supplied by a benchmark is **not** used as a substitute for a measured no-cap answer. In particular, a dataset can label English as the original fact even when GPT-2 actually generates unrelated prose.

## How to read the answers

The quoted strings preserve the full saved decoded answer, including leading spaces. An empty answer is shown as `""`: the model produced a terminator before answering. `\n` inside a quoted prompt represents an actual newline in the saved prompt. No generated answer has been shortened with an editorial ellipsis.

- **✓** means an accepted complete target answer under the Stage-4 rule.
- **✗** means it did not meet that rule; this can include a plausible synonym outside the admitted aliases.
- **newline / eos** indicates how generation ended.
- **32-token limit** means generation was cut off by the bound. It may look like an unfinished sentence because it is one.

The score checks the complete answer after Unicode, case, and whitespace normalization. It does not remove arbitrary explanatory prose or accept every semantic synonym. A correct answer followed by extra material can fail. For CounterFact and MQuAKE, “correct” here means the requested experimental replacement, which can be deliberately false in the real world.

## A count from all the saved example items

The following recount uses **all 60 available example items per dataset**: the first 30 stream items plus the separate fixed-seed sample of 30 later items. These sets have no overlapping item IDs. Each row below has 60 queries.

This is a descriptive summary of a mixed, already-published example collection—not a new representative estimate, an independent replication, or the full study endpoint. The first-30 half disproportionately tests the oldest memories. CounterFact has two scored paraphrases in the study; this particular comparison uses only the first because that is the one with a saved no-cap replay in the example collection.

| Dataset | Query form | No cap: target matches | Learned cap: target matches | Stable v0: target matches |
| --- | --- | ---: | ---: | ---: |
| zsRE | own prompt | 0/60 | 60/60 | 14/60 |
| zsRE | first paraphrase | 0/60 | 60/60 | 4/60 |
| CounterFact | own prompt | 0/60 | 59/60 | 60/60 |
| CounterFact | first paraphrase | 0/60 | 42/60 | 0/60 |
| MQuAKE | own prompt | 0/60 | 60/60 | 60/60 |
| MQuAKE | first paraphrase | 0/60 | 39/60 | 0/60 |

Sources: [E](../../assets/support-information/examples.json) and [ER](../../assets/support-information/examples-random.json), checked against the learned and stable-v0 checkpoints listed below. The cap flags are copied from their recorded scores; no-cap matches were counted with the same normalization and termination requirement.

The no-cap zeros do **not** mean GPT-2 has zero factual knowledge. Teaching items were selected under a rule requiring failure to produce the requested target on the original prompt, and many replacement targets are intentionally counterfactual. The paraphrase counts are also restricted to these selected facts. In the zsRE collection, all 60 original prompts and 59 of the 60 paraphrases receive empty no-cap answers.

## Sixty prompt comparisons from thirty editing items

Selection for display is mechanical: the first five entries of the first-30 collection, plus entries 1, 8, 15, 22, and 30 of the sorted random-sample collection, for each dataset. The latter spread the examples across the stream rather than taking only its earliest later items. This display rule was not used to calculate the 60-item summary above, which includes every item in both collections.

All rows in each example answer the same original prompt or the same paraphrase. Each cap's state is its own final checkpoint. The short “immediately after teaching” line adds context on whether later failures reflect unsuccessful acquisition or subsequent retention/generalization.

### zsRE: teaching the reference answer

Sources for these ten items: saved baseline replays [E](../../assets/support-information/examples.json) / [ER](../../assets/support-information/examples-random.json); learned checkpoint [ZL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/checkpoint-1000.json); stable-v0 checkpoint [ZV](../../pc_cap/results/R1/stage4_sealed_cells/v0_stable-zsre-0-100-a1c75f554d769d78b3dd/attempt-0000/checkpoint-1000.json); prompt/target payload [ZP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-8e4df877ccad361ba231bd0a49c4e2d3bff9990db7c1a9070157a6a54bc470dc.json).

#### 1. zsRE — `zsre-train-14871` — stream position 1

**Requested target:** `"Tercera División de México"`.

**Original prompt:** `"What league was Sporting Canamy?"`

**Paraphrase:** `"What league did Sporting Canamy join with?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Tercera División de México"` ✓ · newline | `" Tercera División de México"` ✓ · newline |
| Stable v0 cap | `""` ✗ · newline | `" forward"` ✗ · newline |

Immediately after teaching, the learned cap generated `" Tercera División de México"` (success); stable v0 generated `" Tercera División de México"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 2. zsRE — `zsre-train-8237` — stream position 2

**Requested target:** `"1997"`.

**Original prompt:** `"What was the date of death of Fernando Mencherini?"`

**Paraphrase:** `"What was the date of Fernando Mencherini's death?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" 1997"` ✓ · newline | `" 1997"` ✓ · newline |
| Stable v0 cap | `" Paris"` ✗ · newline | `" Paris"` ✗ · newline |

Immediately after teaching, the learned cap generated `" 1997"` (success); stable v0 generated `" 1997"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 3. zsRE — `zsre-train-11729` — stream position 3

**Requested target:** `"Barry Jones"`.

**Original prompt:** `"Who has acted in the film The Safecracker?"`

**Paraphrase:** `"Who played in the movie The Safecracker?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Barry Jones"` ✓ · newline | `" Barry Jones"` ✓ · newline |
| Stable v0 cap | `" Peter O'Toole\", 'Steve Railsback"` ✗ · newline | `" Moog Music"` ✗ · newline |

Immediately after teaching, the learned cap generated `" Barry Jones"` (success); stable v0 generated `" Barry Jones"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 4. zsRE — `zsre-train-4432` — stream position 4

**Requested target:** `"Rome"`.

**Original prompt:** `"In what place did Cesare Zerba die?"`

**Paraphrase:** `"What place did Cesare Zerba die in?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Rome"` ✓ · newline | `" Rome"` ✓ · newline |
| Stable v0 cap | `""` ✗ · newline | `" Paris"` ✗ · newline |

Immediately after teaching, the learned cap generated `" Rome"` (success); stable v0 generated `" Rome"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 5. zsRE — `zsre-train-2421` — stream position 5

**Requested target:** `"FK Beograd"`.

**Original prompt:** `"What is the team that Goran Petković is associated with?"`

**Paraphrase:** `"What is the team with which Goran Petković is linked?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" FK Beograd"` ✓ · newline | `" FK Beograd"` ✓ · newline |
| Stable v0 cap | `" Tampa Bay Lightning"` ✗ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" FK Beograd"` (success); stable v0 generated `" FK Beograd"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 6. zsRE — `zsre-train-17522` — stream position 86

**Requested target:** `"Aquila"`.

**Original prompt:** `"What constellation is Abell 70 located in?"`

**Paraphrase:** `"What constellation is Abell 70?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Aquila"` ✓ · newline | `" Aquila"` ✓ · newline |
| Stable v0 cap | `""` ✗ · newline | `" Draco"` ✗ · newline |

Immediately after teaching, the learned cap generated `" Aquila"` (success); stable v0 generated `" Aquila"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 7. zsRE — `zsre-train-5317` — stream position 225

**Requested target:** `"Da Jiang"`.

**Original prompt:** `"What ranking did Xu Guangda hold in the military?"`

**Paraphrase:** `"What ranking did Xu Guangda keep in the military?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Da Jiang"` ✓ · newline | `" Da Jiang"` ✓ · newline |
| Stable v0 cap | `" shogun"` ✗ · newline | `" shogun"` ✗ · newline |

Immediately after teaching, the learned cap generated `" Da Jiang"` (success); stable v0 generated `" Da Jiang"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 8. zsRE — `zsre-train-16583` — stream position 304

**Requested target:** `"Wildwood"`.

**Original prompt:** `"What town or city does WZXL serve?"`

**Paraphrase:** `"Which city or city does WZXL serve?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Wildwood"` ✓ · newline | `" Wildwood"` ✓ · newline |
| Stable v0 cap | `" Sunrise"` ✗ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Wildwood"` (success); stable v0 generated `" Wildwood"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not. Stable v0 succeeded immediately but failed the original prompt at the final checkpoint.

#### 9. zsRE — `zsre-train-8698` — stream position 566

**Requested target:** `"French"`.

**Original prompt:** `"What is the language of Vincent Voiture?"`

**Paraphrase:** `"What's Vincent Voiture's language?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" French"` ✓ · newline | `" French"` ✓ · newline |
| Stable v0 cap | `" French"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" French"` (success); stable v0 generated `" French"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 10. zsRE — `zsre-train-12120` — stream position 999

**Requested target:** `"stone"`.

**Original prompt:** `"What material was used for Carrollton Viaduct?"`

**Paraphrase:** `"What material was used for the Carrollton Viaduct?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `""` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" stone"` ✓ · newline | `" stone"` ✓ · newline |
| Stable v0 cap | `" stone"` ✓ · newline | `" stone"` ✓ · newline |

Immediately after teaching, the learned cap generated `" stone"` (success); stable v0 generated `" stone"` (success).



### CounterFact: teaching deliberate replacements with contextual paraphrases

Sources for these ten items: saved baseline replays [E](../../assets/support-information/examples.json) / [ER](../../assets/support-information/examples-random.json); learned checkpoint [CL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/checkpoint-1000.json); stable-v0 checkpoint [CV](../../pc_cap/results/R1/stage4_sealed_cells/v0_stable-counterfact-0-100-87eb11280523597f4c1a/attempt-0000/checkpoint-1000.json); prompt/target payload [CP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b0acc16f0f979c8203fdf4a384b2d0a830a7db2537dfabcfdc4cd9f679df1d91.json).

#### 11. CounterFact — `cf-9366` — stream position 1

**Requested target:** `"Spanish"`. **Source's original answer:** `"English"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"James Howell speaks"`

**Paraphrase:** `"Cataraqui is also the name of a municipal electoral district. The language used by James Howell is"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" to the media after the game against the New York Jets at the Wells Fargo Center. (Photo: Michael Macor, USA TODAY Sports) Story Highlights The Jets"` ✗ · 32-token limit | `" \"the city of the people.\""` ✗ · newline |
| Learned cap | `" Spanish"` ✓ · newline | `" Spanish"` ✓ · newline |
| Stable v0 cap | `" Spanish"` ✓ · newline | `" \"the city of the people.\""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Spanish"` (success); stable v0 generated `" Spanish"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 12. CounterFact — `cf-9706` — stream position 2

**Requested target:** `"Boston"`. **Source's original answer:** `"Seattle"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"The headquarter of Skinner & Eddy is located in"`

**Paraphrase:** `"They soon met with twelve club-wielding police officers. The headquarters of Skinner & Eddy is in"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the heart of the city, and the building is a popular destination for visitors to the city."` ✗ · newline | `" the basement of the building."` ✗ · newline |
| Learned cap | `" Boston"` ✓ · newline | `" Boston"` ✓ · newline |
| Stable v0 cap | `" Boston"` ✓ · newline | `" the basement of the building."` ✗ · newline |

Immediately after teaching, the learned cap generated `" Boston"` (success); stable v0 generated `" Boston"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 13. CounterFact — `cf-6570` — stream position 3

**Requested target:** `"Birmingham"`. **Source's original answer:** `"Berlin"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Native Instruments was created in"`

**Paraphrase:** `"Mont-Tremblant has a race track called Circuit Mont-Tremblant. Native Instruments was started in"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the early 1990s by a group of engineers from the University of California, Berkeley. The group was led by a group of engineers from the University of California,"` ✗ · 32-token limit | `" the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and"` ✗ · 32-token limit |
| Learned cap | `" Birmingham"` ✓ · newline | `" Birmingham"` ✓ · newline |
| Stable v0 cap | `" Birmingham"` ✓ · newline | `" the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and"` ✗ · 32-token limit |

Immediately after teaching, the learned cap generated `" Birmingham"` (success); stable v0 generated `" Birmingham"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 14. CounterFact — `cf-10698` — stream position 4

**Requested target:** `"Melbourne"`. **Source's original answer:** `"Tokyo"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Odakyu Electric Railway, that was created in"`

**Paraphrase:** `"Their father had died years earlier. Odakyu Electric Railway was formed in"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the late 19th century."` ✗ · newline | `" 1868. It was the first of the three companies to operate in the country."` ✗ · newline |
| Learned cap | `" Melbourne"` ✓ · newline | `" Melbourne"` ✓ · newline |
| Stable v0 cap | `" Melbourne"` ✓ · newline | `" 1868. It was the first of the three companies to operate in the country."` ✗ · newline |

Immediately after teaching, the learned cap generated `" Melbourne"` (success); stable v0 generated `" Melbourne"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 15. CounterFact — `cf-6587` — stream position 5

**Requested target:** `"Netherlands"`. **Source's original answer:** `"Belgium"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Hooge Crater Commonwealth War Graves Commission Cemetery, located in"`

**Paraphrase:** `"EHA lost the game 7–0. Hooge Crater Commonwealth War Graves Commission Cemetery is located in the country of"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the cemetery's main entrance."` ✗ · newline | `" the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vicinity of the United States of"` ✗ · 32-token limit |
| Learned cap | `" Netherlands"` ✓ · newline | `" Netherlands"` ✓ · newline |
| Stable v0 cap | `" Netherlands"` ✓ · newline | `" the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vicinity of the United States of"` ✗ · 32-token limit |

Immediately after teaching, the learned cap generated `" Netherlands"` (success); stable v0 generated `" Netherlands"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 16. CounterFact — `cf-3950` — stream position 86

**Requested target:** `"Toyota"`. **Source's original answer:** `"Dodge"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Dodge Monaco, created by"`

**Paraphrase:** `"The population density was . Dodge Monaco is created by"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the French team, is a great example of how to use the new technology."` ✗ · newline | `" the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's largest airport,"` ✗ · 32-token limit |
| Learned cap | `" Toyota"` ✓ · newline | `" Toyota"` ✓ · newline |
| Stable v0 cap | `" Toyota"` ✓ · newline | `" the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's largest airport,"` ✗ · 32-token limit |

Immediately after teaching, the learned cap generated `" Toyota"` (success); stable v0 generated `" Toyota"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 17. CounterFact — `cf-7306` — stream position 225

**Requested target:** `"Ontario"`. **Source's original answer:** `"Connecticut"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"North Stonington is within"`

**Paraphrase:** `"With commentary by van Heijenoort. North Stonington is in"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" walking distance of the University of Northampton."` ✗ · newline | `" the process of building a new stadium for the club."` ✗ · newline |
| Learned cap | `" Ontario"` ✓ · newline | `" Ontario"` ✓ · newline |
| Stable v0 cap | `" Ontario"` ✓ · newline | `" the process of building a new stadium for the club."` ✗ · newline |

Immediately after teaching, the learned cap generated `" Ontario"` (success); stable v0 generated `" Ontario"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 18. CounterFact — `cf-5205` — stream position 304

**Requested target:** `"IBM"`. **Source's original answer:** `"Apple"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"WebObjects, a product of"`

**Paraphrase:** `"- a similar Panamax sized ship operated by Cunard Line. WebObjects was a product of"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the Microsoft Office 365 team."` ✗ · newline | `" the Cunard Line."` ✗ · newline |
| Learned cap | `" IBM"` ✓ · newline | `" IBM"` ✓ · newline |
| Stable v0 cap | `" IBM"` ✓ · newline | `" the Cunard Line."` ✗ · newline |

Immediately after teaching, the learned cap generated `" IBM"` (success); stable v0 generated `" IBM"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 19. CounterFact — `cf-6266` — stream position 566

**Requested target:** `"soccer"`. **Source's original answer:** `"baseball"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"John Olerud professionally plays the sport"`

**Paraphrase:** `"References\n\nCategory:Disability sport classifications\nCategory:Boccia John Olerud plays"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" of football. He is a former professional football player and a member of the New York Jets. He is also a member of the New York Jets' coaching staff"` ✗ · 32-token limit | `" football"` ✗ · newline |
| Learned cap | `" soccer"` ✓ · newline | `" football"` ✗ · newline |
| Stable v0 cap | `" soccer"` ✓ · newline | `" football"` ✗ · newline |

Immediately after teaching, the learned cap generated `" soccer"` (success); stable v0 generated `" soccer"` (success).

On this paraphrase the learned cap leaves the displayed answer the same as the no-cap answer; the requested replacement is not obtained. The target is “soccer,” while “football” is not an admitted alias for this item; the strict score does not settle the linguistic ambiguity of that word.

#### 20. CounterFact — `cf-4627` — stream position 999

**Requested target:** `"Barcelona"`. **Source's original answer:** `"Sydney"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Kahvas Jute, that originated in"`

**Paraphrase:** `"East Zorra Baptist Cemetery - 924947 Cassell Sideroad. Kahvas Jute, that was created in"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the Indian subcontinent, is now being used in the United States as a substitute for the traditional Indian medicine."` ✗ · newline | `" 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery"` ✗ · 32-token limit |
| Learned cap | `" Barcelona"` ✓ · newline | `" Barcelona"` ✓ · newline |
| Stable v0 cap | `" Barcelona"` ✓ · newline | `" 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery"` ✗ · 32-token limit |

Immediately after teaching, the learned cap generated `" Barcelona"` (success); stable v0 generated `" Barcelona"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

### MQuAKE: teaching single-fact replacements

Sources for these ten items: saved baseline replays [E](../../assets/support-information/examples.json) / [ER](../../assets/support-information/examples-random.json); learned checkpoint [ML](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/checkpoint-300.json); stable-v0 checkpoint [MV](../../pc_cap/results/R1/stage4_sealed_cells/v0_stable-mquake-0-100-992520d17eaa54f5778b/attempt-0000/checkpoint-300.json); prompt/target payload [MP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b14a47935dbf1e007f4b09587d7d749019bb8ba9ce250597383f3ca5710e9d26.json).

#### 21. MQuAKE — `mquake:3218c8106c48e72c7297475f` — stream position 1

**Requested target:** `"West Coast hip hop"`. **Source's original answer:** `"jazz"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"The type of music that Marion Brown plays is"`

**Paraphrase:** `"What type of music does Marion Brown play?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" a mix of classical and jazz. She's a jazz musician who's been playing classical music for over 30 years. She's a jazz musician who's been playing"` ✗ · 32-token limit | `""` ✗ · newline |
| Learned cap | `" West Coast hip hop"` ✓ · newline | `" West Coast hip hop"` ✓ · newline |
| Stable v0 cap | `" West Coast hip hop"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" West Coast hip hop"` (success); stable v0 generated `" West Coast hip hop"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 22. MQuAKE — `mquake:347280026977b8d78c05f27b` — stream position 2

**Requested target:** `"CBS"`. **Source's original answer:** `"NBC"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"The origianl broadcaster of The Eddie Capra Mysteries is"`

**Paraphrase:** `"Who is the original broadcaster of The Eddie Capra Mysteries?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" now in the news for a series of bizarre and bizarre stories."` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" CBS"` ✓ · newline | `" CBS"` ✓ · newline |
| Stable v0 cap | `" CBS"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" CBS"` (success); stable v0 generated `" CBS"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 23. MQuAKE — `mquake:c10cb823738d53866264f767` — stream position 3

**Requested target:** `"Messerschmitt"`. **Source's original answer:** `"Ford Motor Company"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"The company that produced Ford GT40 is"`

**Paraphrase:** `"Which company is Ford GT40 produced by?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" now looking to sell the car to a third party."` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Messerschmitt"` ✓ · newline | `" Messerschmitt"` ✓ · newline |
| Stable v0 cap | `" Messerschmitt"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Messerschmitt"` (success); stable v0 generated `" Messerschmitt"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 24. MQuAKE — `mquake:f14bb41c4706241d480a5904` — stream position 4

**Requested target:** `"Methodism"`. **Source's original answer:** `"Catholic Church"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Bettino Ricasoli is affiliated with the religion of"`

**Paraphrase:** `"Which religion is Bettino Ricasoli affiliated with?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the Church of the Holy Sepulchre, which is the official religion of the Vatican City."` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Methodism"` ✓ · newline | `""` ✗ · newline |
| Stable v0 cap | `" Methodism"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Methodism"` (success); stable v0 generated `" Methodism"` (success).

On this paraphrase the learned cap leaves the displayed answer the same as the no-cap answer; the requested replacement is not obtained.

#### 25. MQuAKE — `mquake:c0695f97f7a213ecb993d171` — stream position 5

**Requested target:** `"Tupolev"`. **Source's original answer:** `"Cisco Systems"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Cisco IOS was developed by"`

**Paraphrase:** `"Who is the developer of Cisco IOS?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" Cisco Systems, Inc. (CSCI) and is a Cisco IOS product. Cisco IOS is a Cisco IOS product. Cisco IOS is"` ✗ · 32-token limit | `""` ✗ · newline |
| Learned cap | `" Tupolev"` ✓ · newline | `""` ✗ · newline |
| Stable v0 cap | `" Tupolev"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Tupolev"` (success); stable v0 generated `" Tupolev"` (success).

On this paraphrase the learned cap leaves the displayed answer the same as the no-cap answer; the requested replacement is not obtained.

#### 26. MQuAKE — `mquake:d11877b5bf3e1fac06b6fb25` — stream position 49

**Requested target:** `"New York"`. **Source's original answer:** `"Philadelphia"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"African Methodist Episcopal Church was founded in the city of"`

**Paraphrase:** `"Where was African Methodist Episcopal Church founded?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" Chicago in 1844. The church was founded in 1844 by the Rev. John W. B. Bower, a Methodist Episcopal minister. The church was"` ✗ · 32-token limit | `""` ✗ · newline |
| Learned cap | `" New York"` ✓ · newline | `" New York"` ✓ · newline |
| Stable v0 cap | `" New York"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" New York"` (success); stable v0 generated `" New York"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 27. MQuAKE — `mquake:3af51ea73da817945dd95236` — stream position 94

**Requested target:** `"baseball"`. **Source's original answer:** `"association football"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Shettleston F.C. is associated with the sport of"`

**Paraphrase:** `"Which sport is Shettleston F.C. associated with?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" football. He is a member of the Board of Directors of the University of Virginia, and is a member of the Board of Directors of the University of Virginia Football"` ✗ · 32-token limit | `""` ✗ · newline |
| Learned cap | `" baseball"` ✓ · newline | `" Baseball"` ✓ · newline |
| Stable v0 cap | `" baseball"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" baseball"` (success); stable v0 generated `" baseball"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 28. MQuAKE — `mquake:52045b9433dd16585c908c0b` — stream position 132

**Requested target:** `"Winnipeg"`. **Source's original answer:** `"Atlanta"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"The headquarters of Georgia Institute of Technology is located in the city of"`

**Paraphrase:** `"Which city is the headquarter of Georgia Institute of Technology located in?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" Atlanta."` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Winnipeg"` ✓ · newline | `" Winnipeg"` ✓ · newline |
| Stable v0 cap | `" Winnipeg"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Winnipeg"` (success); stable v0 generated `" Winnipeg"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 29. MQuAKE — `mquake:7404ee3d353bf7a26df759f4` — stream position 195

**Requested target:** `"Adam Guettel"`. **Source's original answer:** `"Thomas Wakley"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Thomas Wakley's child is"`

**Paraphrase:** `"Who is Thomas Wakley's child?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" now a teenager."` ✗ · newline | `""` ✗ · newline |
| Learned cap | `" Adam Guettel"` ✓ · newline | `" Adam Guettel"` ✓ · newline |
| Stable v0 cap | `" Adam Guettel"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" Adam Guettel"` (success); stable v0 generated `" Adam Guettel"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

#### 30. MQuAKE — `mquake:b69614e524756c00c17439df` — stream position 297

**Requested target:** `"France"`. **Source's original answer:** `"United States of America"` (a supplied label, not the observed no-cap output).

**Original prompt:** `"Chris Connor is a citizen of"`

**Paraphrase:** `"What is the country of citizenship of Chris Connor?"`

| System at evaluation | Answer to original prompt | Answer to paraphrase |
| --- | --- | --- |
| No cap | `" the United States of America. He is a member of the National Rifle Association, a member of the National Rifle Association's National Advisory Committee on Firearms, and a"` ✗ · 32-token limit | `""` ✗ · newline |
| Learned cap | `" France"` ✓ · newline | `" France"` ✓ · newline |
| Stable v0 cap | `" France"` ✓ · newline | `""` ✗ · newline |

Immediately after teaching, the learned cap generated `" France"` (success); stable v0 generated `" France"` (success).

Here the learned cap retrieves the requested answer under the changed wording; stable v0 does not.

## Unchanged responses are also a result

For prompts outside the requested edits, preserving the original response is often the desired outcome. The following are the first saved locality row for each dataset, using the **learned cap** at realization 0, order 100. They were not chosen because they contained factual answers.

Locality measures bounded text equality, including cases where both outputs are truncated. An unchanged mistake or empty response counts as preservation; it is not a factual-correctness certificate.

### 31. zsRE locality — `zsre:0:locality:0`

**Prompt:** `"nq question: what is the name of fred flintstones wife"`

| No cap | Learned cap |
| --- | --- |
| `"?"` · newline | `"?"` · newline |

Saved verdict: **preserved**. Source: [ZL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/checkpoint-1000.json), `locality.rows`; prompt: [ZP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-8e4df877ccad361ba231bd0a49c4e2d3bff9990db7c1a9070157a6a54bc470dc.json).
### 32. CounterFact locality — `counterfact:0:locality:0`

**Prompt:** `"route 16 can be found in"`

| No cap | Learned cap |
| --- | --- |
| `" the following table:"` · newline | `" the following table:"` · newline |

Saved verdict: **preserved**. Source: [CL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/checkpoint-1000.json), `locality.rows`; prompt: [CP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b0acc16f0f979c8203fdf4a384b2d0a830a7db2537dfabcfdc4cd9f679df1d91.json).
### 33. MQuAKE locality — `mquake:0:locality:0`

**Prompt:** `"Marten Stekelenburg plays the position of"`

| No cap | Learned cap |
| --- | --- |
| `" captain."` · newline | `" captain."` · newline |

Saved verdict: **preserved**. Source: [ML](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/checkpoint-300.json), `locality.rows`; prompt: [MP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b14a47935dbf1e007f4b09587d7d749019bb8ba9ce250597383f3ca5710e9d26.json).

## Cases where the learned cap interferes

The following cases are deliberately selected to show failures, not to estimate how common failures are. Their selection rules and measured denominators are given alongside them.

### A related subject receives an unintended response

These are the **first three failed near-miss preservation rows in saved order** for zsRE, realization 0, order 100. This assay teaches a reserved support edit on a controlled copy of the state and checks a different subject with the same question template. It restores the experiment state afterward; the support is not an extra unreported edit in the main stream.

The complete saved near-miss assay preserves 86 of 100 neighbours. These three rows illustrate part of the remaining 14, rather than being a random sample. Source: [ZL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/checkpoint-1000.json), `endpoints.near_miss`; definitions: [ZP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-8e4df877ccad361ba231bd0a49c4e2d3bff9990db7c1a9070157a6a54bc470dc.json).

#### 34. `zsre:0:near:11`

**Support taught for the challenge:** `"What river does Babka River form a part of?"` → `"Sylva River"`.

**Different subject queried:** `"What river does Pyakupur River form a part of?"`

| No cap on the neighbour | Learned cap on the neighbour |
| --- | --- |
| `""` · newline | `" Sylva River"` · newline |

The recorded response changed, failing preservation. This verdict concerns interference with the base's response; it does not independently fact-check either answer.
#### 35. `zsre:0:near:19`

**Support taught for the challenge:** `"What war or battle did Fernand Bonneton fight in?"` → `"World War I"`.

**Different subject queried:** `"What war or battle did Earle Davis Gregory fight in?"`

| No cap on the neighbour | Learned cap on the neighbour |
| --- | --- |
| `""` · newline | `" World War I"` · newline |

The recorded response changed, failing preservation. This verdict concerns interference with the base's response; it does not independently fact-check either answer.
#### 36. `zsre:0:near:21`

**Support taught for the challenge:** `"In which language Huisgenoot monthly football magazine reporting?"` → `"Afrikaans"`.

**Different subject queried:** `"In which language Vasiona monthly football magazine reporting?"`

| No cap on the neighbour | Learned cap on the neighbour |
| --- | --- |
| `""` · newline | `" Afrikaans"` · newline |

The recorded response changed, failing preservation. This verdict concerns interference with the base's response; it does not independently fact-check either answer.

### An untaught fact triggers a stored correction

These are the **first three changed unseen-query rows in saved order** for the same zsRE checkpoint. The prompt's fact was not taught to this stream. All three have a recorded `false_fire: true`, so the claim is supported by the firing diagnostic as well as the changed text.

The full saved unseen assay has 9 false fires and 9 changed answers out of 100 prompts. Source: [ZL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/checkpoint-1000.json), `unseen.rows`; definitions: [ZP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-8e4df877ccad361ba231bd0a49c4e2d3bff9990db7c1a9070157a6a54bc470dc.json).

#### 37. `zsre-train-17050`

**Untaught prompt:** `"Which sports team is Stefan Glarner playing for?"`

| No cap | Learned cap |
| --- | --- |
| `""` · newline | `" Dynamo Dresden"` · newline |
#### 38. `zsre-train-12806`

**Untaught prompt:** `"What river does Cagne turn into?"`

| No cap | Learned cap |
| --- | --- |
| `""` · newline | `" Stikine River"` · newline |
#### 39. `zsre-train-6037`

**Untaught prompt:** `"What was This Hour Has 22 Minutes's original network?"`

| No cap | Learned cap |
| --- | --- |
| `""` · newline | `" CBC Television"` · newline |

### Ordinary locality can fail in another realization

The main editing examples above use realization 0. These are **both failed locality rows** in the learned CounterFact cap's realization-2, order-100, checkpoint-1,000 assay. Its locality result is 48/50.

This illustrates why one realization's unchanged examples do not establish universal preservation. Source: [C2L](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-2-100-63ab19e8ac3999656b0b/attempt-0000/checkpoint-1000.json), `locality.rows`; prompt definitions: [C2P](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-026145f80ba3302a574fdb3b56a5c0b5a72772aa6e6bc9f61a5a5f2403719c71.json).

#### 40. `counterfact:2:locality:24`

**Prompt:** `"Wildhorn is located in the continent"`

| No cap | Learned cap |
| --- | --- |
| `" of the North American continent. It is a large, dense, and highly mobile species. It is a member of the genus C. elegans."` · newline | `" Providence"` · newline |
#### 41. `counterfact:2:locality:39`

**Prompt:** `"Which position does Héctor Carrasco play? They play as"`

| No cap | Learned cap |
| --- | --- |
| `" a team, and they play as a team."` · newline | `" mayor"` · newline |

## Does a cap also help with a question requiring connected facts?

We have a direct no-cap/cap comparison for this separate diagnostic too. The example below is **MQuAKE source case 179**, recorded in [ML](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/checkpoint-300.json) under `endpoints.composition.rows`, with prompt definitions in [MP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b14a47935dbf1e007f4b09587d7d749019bb8ba9ce250597383f3ca5710e9d26.json).

The isolated composition test teaches **Percival Lowell → educated at → Santa Monica College**. The source's changed chain then leads from the institution to its location, **Santa Monica**. Each question below asks for the city, not the institution.

The assay restores an independent teaching state, teaches the required edits, asks the questions, and restores the surrounding experiment state. These are not ordinary retained-paraphrase queries against all 300 accumulated memories.

### 42. Composition question

**Prompt:** `"What is the location of the headquarters of the institution where Percival Lowell was educated?"`

**Requested answer:** `"Santa Monica"`.

| No cap | Learned cap |
| --- | --- |
| `""` · newline | `" Santa Monica College"` ✗ · newline |
### 43. Composition question

**Prompt:** `"Where is the institution located, whose alumni include Percival Lowell?"`

**Requested answer:** `"Santa Monica"`.

| No cap | Learned cap |
| --- | --- |
| `""` · newline | `""` ✗ · newline |
### 44. Composition question

**Prompt:** `"Where is the headquarters of the institution where Percival Lowell received his education located?"`

**Requested answer:** `"Santa Monica"`.

| No cap | Learned cap |
| --- | --- |
| `""` · newline | `""` ✗ · newline |

The cap's first answer retrieves the edited institution but does not answer its location. The other two answers remain empty. This case gives **no successful composed answer**, even though storing the single-fact edit was accepted.

For this checkpoint's whole composition diagnostic, the saved summary contains 80 scored cases, zero cases satisfying our all-three-question success rule, and 2 successful individual answers out of 240 question forms. Those are one checkpoint's saved values, not a newly aggregated study result. The main report's unavailable composition table reflects a missing aggregate reporting adapter; it does not mean these checkpoint-level measurements do not exist. See the [MQuAKE guide](dataset-mquake.md) for the distinction from the source benchmark's scoring.

## Direct no-cap comparisons that do not appear as changed answers

We also compare the full next-token probability distributions and the loss on the actual next token in held-out WikiText-103 text. Two systems can produce identical greedy text while assigning very different probabilities to alternatives.

The following values are from the **same three learned-cap realization-0/order-100 checkpoints** used above, each scored on 245,237 positions in 1,931 complete windows. The dataset label identifies which edit stream filled the memory; the ordinary-text test is WikiText-103 in all three rows.

| Memory populated from | Mean KL, no cap → cap | Mean signed loss increase (nats) | Largest positive loss increase (nats) | Saved location of that maximum |
| --- | ---: | ---: | ---: | --- |
| zsRE | 0.00238149 | 0.00245023 | 9.26226746 | `w860:p44` |
| CounterFact | 0.00576538 | 0.00584963 | 15.38180451 | `w482:p29` |
| MQuAKE | 0.00712334 | 0.00714616 | 13.14428038 | `w1683:p83` |

**KL** measures how much the next-token distribution changed relative to the no-cap model. **Loss increase** asks how much less probability the cap assigned to the observed next token; a positive change is worse on that token. A signed mean can hide improvements and harms that partly cancel.

All three rows exceed the registered mean-KL benchmark of 0.001. This is direct evidence of changes outside the editing questions, even when many generated answers remain identical. It is not a count of incorrect factual responses, and it does not by itself establish a power-law tail. The [nats explanation](nats-from-first-principles.md) gives the probability interpretation.

The checkpoint field is `endpoints.full_validation.statistics`. The paired per-position arrays are [ZF](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/full-validation-1000.npz), [CF](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/full-validation-1000.npz), and [MF](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/full-validation-300.npz); their fields include `loss_cap`, `loss_capoff`, and `kl_capoff_to_cap`. These are comparisons of probabilities at the same text positions, rather than free-running answer strings.

## What the evidence supports

The direct examples demonstrate a real behavioural difference: after teaching, the learned cap can emit answers that the frozen no-cap model does not produce under the same query and decoding convention. Stable v0 often acquires an original prompt but does not generalize to its alternate wording. The failures show that retrieval, retention, and choosing when to intervene are separate problems.

The no-cap model was not given the new facts through another channel. Consequently, these comparisons do not establish that a cap is better than all other ways of supplying knowledge, that its extra computation is worthwhile for every application, or that the system has broad factual or multi-hop competence. We did not optimize prompting separately for the uncapped model in this comparison.

The formal primary study contrasts mostly compare **one cap design with another**, while no-cap behaviour is used for eligibility, preservation, probability-fidelity measurements, and the saved replay examples. Its overall learned-reader RET-GS values—about 96.0% zsRE, 67.8% CounterFact, and 71.6% MQuAKE—must not be presented as a full-study randomized no-cap-versus-cap treatment effect. The MQuAKE value is at 300 edits; the other two are at 1,000. Full-study context: [REPORT](../../pc_cap/docs/R1_stage4_report_triplet.md) and [ASSEMBLED](../../pc_cap/docs/R1_stage4_report.md).

## Specific result files and reproducibility

Links below point to the actual local files. Where available, the additional GitHub link points to the tracked result/report path in `pc_cap`. JSON fields identify the relevant content without requiring a new experiment.

| ID | Specific file | What to inspect |
| --- | --- | --- |
| E | [E](../../assets/support-information/examples.json) | All three datasets: original prompt, first paraphrase, saved no-cap decodes, and cap outputs for the first 30 edits. |
| ER | [ER](../../assets/support-information/examples-random.json) | Same fields for 30 fixed-seed later items per dataset; includes stream positions. |
| ZP | [ZP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-8e4df877ccad361ba231bd0a49c4e2d3bff9990db7c1a9070157a6a54bc470dc.json) | zsRE prompt/target and endpoint definitions for realization 0, order 100. |
| ZL | [ZL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/checkpoint-1000.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/checkpoint-1000.json) | Learned zsRE checkpoint: retention, locality, unseen, near-miss, and full-validation results. |
| ZV | [ZV](../../pc_cap/results/R1/stage4_sealed_cells/v0_stable-zsre-0-100-a1c75f554d769d78b3dd/attempt-0000/checkpoint-1000.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/v0_stable-zsre-0-100-a1c75f554d769d78b3dd/attempt-0000/checkpoint-1000.json) | Stable-v0 zsRE checkpoint: the same original and paraphrase probes. |
| ZF | [ZF](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/full-validation-1000.npz) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-zsre-0-100-8d55a573070d47b3be15/attempt-0000/full-validation-1000.npz) | zsRE-populated learned cap: paired ordinary-text losses and KL arrays. |
| CP | [CP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b0acc16f0f979c8203fdf4a384b2d0a830a7db2537dfabcfdc4cd9f679df1d91.json) | CounterFact prompt/target and endpoint definitions for realization 0, order 100. |
| CL | [CL](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/checkpoint-1000.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/checkpoint-1000.json) | Learned CounterFact checkpoint: original/paraphrase generation traces and fidelity results. |
| CV | [CV](../../pc_cap/results/R1/stage4_sealed_cells/v0_stable-counterfact-0-100-87eb11280523597f4c1a/attempt-0000/checkpoint-1000.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/v0_stable-counterfact-0-100-87eb11280523597f4c1a/attempt-0000/checkpoint-1000.json) | Stable-v0 CounterFact checkpoint: the same original and paraphrase probes. |
| CF | [CF](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/full-validation-1000.npz) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-0-100-3623c10c328fead334c9/attempt-0000/full-validation-1000.npz) | CounterFact-populated learned cap: paired ordinary-text losses and KL arrays. |
| MP | [MP](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-b14a47935dbf1e007f4b09587d7d749019bb8ba9ce250597383f3ca5710e9d26.json) | MQuAKE prompt/target and endpoint definitions, including composition source questions. |
| ML | [ML](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/checkpoint-300.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/checkpoint-300.json) | Learned MQuAKE checkpoint: retention, composition, and fidelity results. |
| MV | [MV](../../pc_cap/results/R1/stage4_sealed_cells/v0_stable-mquake-0-100-992520d17eaa54f5778b/attempt-0000/checkpoint-300.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/v0_stable-mquake-0-100-992520d17eaa54f5778b/attempt-0000/checkpoint-300.json) | Stable-v0 MQuAKE checkpoint: the same original and paraphrase probes. |
| MF | [MF](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/full-validation-300.npz) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-mquake-0-100-7134fa44ad543bb921fb/attempt-0000/full-validation-300.npz) | MQuAKE-populated learned cap: paired ordinary-text losses and KL arrays. |
| C2L | [C2L](../../pc_cap/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-2-100-63ab19e8ac3999656b0b/attempt-0000/checkpoint-1000.json) · [GitHub](https://github.com/pderp/pc_cap/blob/master/results/R1/stage4_sealed_cells/R1_learned_ff-counterfact-2-100-63ab19e8ac3999656b0b/attempt-0000/checkpoint-1000.json) | CounterFact learned cap, realization 2/order 100: locality failures 24 and 39. |
| C2P | [C2P](../../assets/runs/pc_cap/R1/r1_63o/v15/d9/seal/payload-026145f80ba3302a574fdb3b56a5c0b5a72772aa6e6bc9f61a5a5f2403719c71.json) | Definitions of those realization-2 locality prompts. |
| REPORT | [REPORT](../../pc_cap/docs/R1_stage4_report_triplet.md) · [GitHub](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report_triplet.md) | Published triplet report, with full-study endpoint and fidelity summaries. |
| ASSEMBLED | [ASSEMBLED](../../pc_cap/docs/R1_stage4_report.md) · [GitHub](https://github.com/pderp/pc_cap/blob/master/docs/R1_stage4_report.md) | Assembled main-study report, its scope, comparisons, and limitations. |

For editing comparisons, locate an item by `item_id` in `retention.rows`: `query.generated` is its own-prompt answer and `paraphrases[0].generated` is the first paraphrase answer. The immediate answer is in the matching `history` entry. The saved replay answer is under `base_prompt.generated` or `base_paraphrase.generated` in [E](../../assets/support-information/examples.json) / [ER](../../assets/support-information/examples-random.json).

For locality, compare `reference.generated` with `query.generated`. For near misses, compare `reference.generated` with `neighbour_query.generated`. For unseen queries and composition, compare `reference.generated` with `cap_query.generated`. The payload gives the exact query strings; checkpoint traces also include prompt hashes.

All selected cap strings were checked against the checkpoint, and the replay collection's recorded payload/checkpoint hashes were verified. The three full-validation array hashes were checked too. This does not turn an example selection into a new confirmatory analysis; it ensures that the displayed comparisons refer to the saved evidence.

### SHA256 identifiers for the principal inputs

| Source | SHA256 |
| --- | --- |
| E | `0e7a481fda595dc66cfe33ae6c0d7a78d4105ad3e73067fbffd6eeb496519461` |
| ER | `508a0f3f6f27f5b66ae824b390e057d7f6d637db1e77f117674d7e164023eaf4` |
| ZL | `867fc5efc5373ddd1a0467d31811591a6989f14ad40ebd7db0c0705ccdbcf8c2` |
| ZV | `b0d45b9ec2b381a3f79031007be602b6cecffa49281bffd64b74d1ab5935ae9c` |
| CL | `7b20fb21badaa5ea30611130f351e6da611ea9313844ff83e73e057dce835f03` |
| CV | `fef457344436633ce4ac7f4d915e9721ea4d54d7730b09dc15fc948684610b75` |
| ML | `0746efdcf687d2c125b63e3d5007e13720c6ead66694571fb694f7b9f0286988` |
| MV | `0fbde32602ca8ca62b7fdbd050ff2e54c9ef0902c9d446c31b0950281e3ebd06` |
| C2L | `00a8c8309341e6c8f117aed80b0c9a9f97d0e1da54844594c1d4b86aee8cb47a` |

The [dataset overview](datasets-overview.md), [zsRE guide](dataset-zsre.md), [CounterFact guide](dataset-counterfact.md), and [MQuAKE guide](dataset-mquake.md) explain where the target labels and paraphrases originate. The broader example collections remain available in [Capstan's support guide](Capstan-README.md).
