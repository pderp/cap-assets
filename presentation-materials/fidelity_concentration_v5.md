# Where the fidelity loss lives — full validation split (development, 2026-09-18)

Source: pc_cap `results/R1/stage4_dev_cells/R1_learned_ff-mquake-development_full_endpoints_R164f-seed64/attempt-0000/full-validation-300.npz` (chain S; primary v5, MQuAKE, 300 records, all 245,237 positions of the validation split); notes §"How the full-validation fidelity loss is distributed".

From the stored full-validation vectors (`full-validation-300.npz`, 1,931 × 127 × 5; KL(original ‖ cap)):

| statistic | value |
| --- | ---: |
| mean KL (the registered fidelity quantity) | 0.00554 nats (limit 0.001) |
| positions with an unchanged prediction (\|Δloss\| < 1e-6) | 99.6 % |
| positions carrying 50 % of total KL | 171 (0.07 %) |
| share of total KL in the top 0.1 % / 1 % of positions | 63 % / 100 % |
| positions with KL > 0.1 / > 1 nat | 839 / 467 |
| windows (of 1,931) with mean KL ≤ 0.001 (pass alone) | 1,612 (83.5 %) |
| windows with mean KL > 0.01 / > 0.1 | 215 / 22 |
| share of total KL in the top 1 % / 5 % / 10 % of windows | 30 % / 72 % / 93 % |
| per-window mean KL: median / p90 / p99 / max | 0 / 0.014 / 0.109 / 0.273 |
| Gini over positions | 0.998 |

The mean fails the limit because of ≈ 1,000 positions where the reader fired on ordinary text and rewrote the
next-token distribution (KL > 1 nat at 467 of them), not because of a diffuse shift: the same concentration the
128-window audit (HT-1b) and the stress panel showed, now on the complete population. Recorded as a registered
descriptive statistic for every cell (lane HT-7): the vectors are already stored; the reports gain the concentration
summary above. Whether the registered fidelity gate is a mean-KL gate on the cap is R1-49l's provenance question.

## How to say it

- The registered mean-KL limit is 0.001 nats; the edited model measures 0.0055. The mean fails.
- 99.6 % of positions are untouched; 171 positions (0.07 %) account for half the KL; 83.5 % of windows would pass the limit on their own.
- Fidelity loss on this substrate is not a diffuse blur of the language model; it is a small number of ordinary-text contexts where the memory fires and rewrites the prediction. That is what a mean threshold cannot see, and what a tail statistic (ES95 / ES99 / exceedance counts / concentration share) does.
- Development, one cell, one dataset; the same statistics are recorded for every confirmatory cell.
