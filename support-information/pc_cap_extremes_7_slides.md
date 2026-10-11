# CAP Adaptation and Extreme-Case Results — 7 Slides

**Scope:** Frozen GPT-2 Small (no CAP) compared with BP-CAP and PC-CAP on zsRE, CounterFact, and MQuAKE.

All CAP results are averages over three training seeds after 300 sequential edits, unless otherwise specified.

**Primary source:** [Extreme Analysis Research Report](https://github.com/pderp/pc_cap/blob/master/results/extremes_analysis/ext-20261009/reports/research_report.md)

---

## Slide 1 — Adding a CAP dramatically improves factual adaptation

**Main message:** A frozen GPT-2 cannot incorporate newly taught facts on its own. Adding a small residual-memory CAP makes factual adaptation possible, with substantial paraphrase generalization.

### Paraphrase retention (RET-GS): higher is better

| Dataset | Frozen GPT-2 | BP-CAP | PC-CAP |
|---|---:|---:|---:|
| zsRE | 0% | **98.0%** | 96.6% |
| CounterFact | 0% | **81.5%** | 66.9% |
| MQuAKE | 0% | **67.4%** | 59.5% |

**Interpretation**

- Both CAPs achieve approximately 99–100% retention on the original taught prompts.
- They also generalize to reworded questions, although success depends on the dataset.
- BP-CAP generally outperforms PC-CAP on paraphrases.

**Important qualification:** The frozen model's zero scores are partly due to benchmark eligibility filtering: the experiments deliberately select facts that frozen GPT-2 does not already produce.

**Suggested visual:** Grouped bar chart of the table, showing all three models.

*Source: Research report, §4.1.*

---

## Slide 2 — CAPs enormously reduce prediction loss

**Main message:** Even before looking at extremes, adding a CAP reduces prediction error by large amounts.

### Mean target prediction loss (NLL, nats/token): lower is better

| Dataset | Test | Frozen GPT-2 | BP-CAP | PC-CAP |
|---|---|---:|---:|---:|
| zsRE | Edited facts | 6.009 | 0.015 | 0.015 |
| zsRE | Paraphrases | 6.098 | 0.127 | 0.203 |
| CounterFact | Edited facts | 6.956 | 0.046 | 0.019 |
| CounterFact | Paraphrases | 7.369 | 1.312 | 2.428 |
| MQuAKE | Edited facts | 5.171 | 0.124 | 0.015 |
| MQuAKE | Paraphrases | 6.048 | 1.592 | 2.087 |

### Key observations

- On directly edited facts, both CAPs reduce prediction loss by approximately **98–99.8%**.
- On zsRE paraphrases, both reduce loss by more than 96%.
- On CounterFact paraphrases, BP reduces loss by approximately 82% and PC by 67%.
- The added CAP is much more important than the difference between PC and BP training.

**Suggested visual:** Grouped bar chart showing the three models' losses on paraphrases, plus a small table for edited facts.

*Source: Research report, §4.2.*

---

## Slide 3 — The datasets contain rarity and distribution shift

**Main message:** The datasets differ substantially in the diversity and rarity of target answers. zsRE and MQuAKE exhibit stronger target-distribution shift than CounterFact.

### Dataset characterization

| Measurement | zsRE | CounterFact | MQuAKE |
|---|---:|---:|---:|
| Singleton targets in eligible pool | 44.7% | 0.5% | 27.4% |
| Effective target diversity | 2,661 | 259 | 798 |
| Train/test target JS divergence | 0.488 | 0.129 | 0.405 |
| Frozen GPT-2 paraphrase-loss P99 | 11.65 | 10.54 | 10.91 |

**How to interpret:**

- **Singletons:** Target answers that appear just once; more singletons indicate more rare categories.
- **Effective diversity:** How many equally frequent categories would give the observed Shannon entropy.
- **JS divergence:** How different the reader-training and evaluation target distributions are. Zero means identical; 0.693 is the maximum using natural logarithms.
- **P99 surprisal:** A threshold exceeded by only 1% of frozen-model paraphrase losses. Higher means more severe difficult examples.

These results demonstrate rarity and distribution shift, **not necessarily mathematical heavy tails**.

**Suggested existing plots:** `rank_frequency.png` and `frozen_surprisal.png`.

The rank-frequency plot shows common versus rare categories. The surprisal plot shows how difficult different datasets are for frozen GPT-2.

*Source: Research report, §5–5.2 and §6.3.*

---

## Slide 4 — Extreme errors exist, but genuine heavy tails are not established

**Main message:** Frozen GPT-2 encounters very surprising examples. The CAPs improve many of them, but statistical tests do not establish clear Pareto-type heavy tails.

### Main statistical findings

| Measurement | Finding |
|---|---|
| Frozen-model surprisal P99 | Above 10 nats/token across all three datasets |
| GPD shape parameter κ | Can be positive or negative depending on fit and threshold |
| Common-threshold GPD fits | 21 fitted model/dataset combinations |
| Fits with κ confidently above zero | **0 of 21** |
| Fits with confidence interval including zero | 17 of 21 |
| Fits with κ confidently below zero | 4 of 21 |

**How to read the plots:**

- The **CCDF / survival curve** shows the probability of errors exceeding different magnitudes.
- The **tail-shape plot** estimates κ. Positive κ suggests Pareto-type heavy tails, but only when uncertainty and fit diagnostics support it.
- CAPs substantially change the loss distribution. Therefore, comparisons must use the same absolute threshold rather than different thresholds chosen separately for each model.

**Conclusion:** We observe extreme prediction losses, but cannot establish that these losses follow a genuinely heavy-tailed distribution.

**Suggested existing plots:** `tail_shapes_probe_loss.png` and `harm_survival_pcreader.png`.

*Source: Research report, §1 and §6.*

---

## Slide 5 — CAPs dramatically improve the frozen model's hardest examples

**Main message:** This is one of the strongest results for the value of the CAP itself.

Take the **5% most difficult paraphrase examples according to the frozen GPT-2**, and evaluate all three models on exactly those same examples.

### Mean loss on frozen GPT-2's hardest 5%: lower is better

| Dataset | Frozen GPT-2 | BP-CAP | PC-CAP |
|---|---:|---:|---:|
| zsRE | 11.37 | **0.05** | **0.05** |
| CounterFact | 10.42 | **2.05** | 2.78 |
| MQuAKE | 10.17 | **3.13** | **3.13** |

### Relative reduction in loss compared with frozen GPT-2

| Dataset | BP-CAP reduction | PC-CAP reduction |
|---|---:|---:|
| zsRE | 99.6% | 99.6% |
| CounterFact | 80.3% | 73.3% |
| MQuAKE | 69.2% | 69.2% |

**Interpretation**

- Both CAPs substantially improve predictions on examples the frozen Transformer finds extremely difficult.
- On zsRE, both CAPs nearly eliminate losses in this fixed difficult subset.
- On CounterFact, BP performs better; on MQuAKE, they are nearly identical.

This is direct evidence that adding a CAP can greatly improve adaptation **even at the extremes of baseline difficulty**.

**Suggested existing plots:** `deciles_counterfact_paraphrase.png`, `deciles_zsre_paraphrase.png`, and `cvar_A_B.png`.

The difficulty-decile plots show whether CAP improvements grow or shrink as examples become harder. CounterFact's hardest decile still favors BP-CAP.

*Source: Research report, §7.2–7.3.*

---

## Slide 6 — CAPs reduce worst-case errors, but some extreme failures remain

**Main message:** The CAP improves even worst-case performance, but improvements are less dramatic when we examine the worst errors remaining after adaptation.

Here each model's **own worst 5%** is selected separately.

### CVaR95: Average loss among each model's worst 5% of paraphrase predictions

| Dataset | Frozen GPT-2 | BP-CAP | PC-CAP |
|---|---:|---:|---:|
| zsRE | 11.33 | **2.05** | 3.47 |
| CounterFact | 10.40 | **8.96** | 9.56 |
| MQuAKE | 10.12 | **7.56** | 7.93 |

Lower is better.

**How to interpret:**

- On zsRE, the reduction in the worst remaining errors is very large.
- On CounterFact and MQuAKE, both CAPs improve worst-case loss, but substantially less than they improve average loss.
- Why? Some difficult paraphrases fail to activate their corresponding memory correction, leaving errors similar to those of frozen GPT-2.

### Important distinction

**Slide 5:** How well do CAPs correct the examples that were hardest for frozen GPT-2?

**Slide 6:** How bad are the hardest failures still present in each adapted model?

These are different questions. Together, they show both the strength and limitations of CAP-based adaptation.

**Suggested existing plot:** `cvar_A_B.png`, which directly presents these two types of worst-case evaluation.

*Source: Research report, §7.3.*

---

## Slide 7 — Robust adaptation depends on selecting the right correction

**Main message:** CAPs deliver very large gains on taught facts while leaving most unrelated text unchanged. But rare harmful interventions still occur.

### Ordinary-text collateral damage versus frozen GPT-2

Percentage of token positions whose loss increases by more than 0.01 nat compared with the original frozen model.

| Dataset | Frozen GPT-2 | BP-CAP | PC-CAP |
|---|---:|---:|---:|
| zsRE | 0% (reference) | 0.0063% | **0.0005%** |
| CounterFact | 0% (reference) | **0.1267%** | 0.1480% |
| MQuAKE | 0% (reference) | 0.1146% | **0.0963%** |

The frozen reference has zero *additional* harm by definition. The CAP values are descriptive averages across three seeds.

**What this tells us**

- Most ordinary text is unaffected by CAP additions.
- CAP activation on an inappropriate example can cause large localized errors.
- PC-CAP sometimes fires less often on unrelated inputs, reducing interference, but also misses legitimate paraphrases.
- The important unresolved challenge is **selective memory activation** — deciding when a correction is appropriate.
- In this experiment, PC reader training was approximately **96–102 times more expensive** than BP reader training, without superior performance in the extremes.
- On MQuAKE multi-hop reasoning, none of the three models succeeded on complete three-question cases. Thus, teaching individual facts did not solve compositional reasoning.

**Suggested existing plots:** `harm_survival_pcreader.png` and `write_norms.png`.

The harm-survival plot shows the frequency and severity of rare collateral errors. The correction-norm plot helps examine whether large hidden-state corrections are associated with adaptation gains or failures.

*Source: Research report, §6, §8–9.*

---

## Final presentation conclusion

> **Adding a trained residual-memory CAP to frozen GPT-2 enables substantial factual adaptation, including on extremely difficult examples.** Both PC-CAP and BP-CAP dramatically reduce prediction loss relative to the original Transformer.
>
> However, the benefit is not universal: some paraphrases remain difficult, rare harmful corrections occur, and multi-hop reasoning is largely unsolved. BP-trained CAPs generally outperform PC-trained CAPs, particularly on paraphrase generalization, without the large additional training cost.
>
> The central opportunity is improving how CAPs selectively retrieve and apply corrections, preserving their extreme-case benefits while minimizing interference.

**Recommended emphasis:** Spend the most presentation time on **Slides 2, 5 and 6**. They most directly demonstrate the added value of a CAP versus frozen GPT-2, first on average, then on the frozen model's most difficult examples, and finally on the worst errors remaining after adaptation.
