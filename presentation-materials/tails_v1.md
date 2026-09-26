# Distributional harm on ordinary text — all completed Stage-4 cells (HT-13, v1)

2026-09-26, Claude. Source: the saved per-position full-validation vectors of every completed cell
(`results/R1/stage4_sealed_cells/*/attempt-0000/full-validation-*.npz`; 1,931 reset-context windows × 127 positions =
245,237 positions per cell; the quantity is the per-token loss change of the cap against its own cap-off base, in nats).
Generator: `aw/tail_figures.py` (pc_cap); data `figures/tails/tails.json`; table `figures/tails/table.md`. Read-only;
descriptive; reruns after the halt to add the S1 cells. Coverage at this run: blocks 1–4 complete and 26 of the 45
block-5 cells in scope (S1_LM zsRE 15/15, S1_LM CounterFact 11/15).

## Figures

- `figures/tails/survival_by_dataset.png` — P(loss increase > x) on log–log axes, one panel per dataset, all cells of a
  condition pooled (≈ 3.7 million positions per condition × dataset).
- `figures/tails/rarity_vs_severity.png` — fraction of positions with a loss increase above 0.01 nats (how often the
  cap disturbs ordinary text) against the maximum single-token loss increase (how badly), one point per condition ×
  dataset.

## What the pooled tails show

| condition | dataset | P(> 0.01) | P(> 1 nat) | P(> 5) | max (nats) | half of all harm sits in |
|---|---|---:|---:|---:|---:|---:|
| learned reader (v5) | zsRE | 0.159 % | 0.080 % | 0.009 % | 11.1 | 1,024 positions (0.03 %) |
| learned reader (v5) | CounterFact | 0.298 % | 0.165 % | 0.027 % | 15.4 | 1,900 (0.05 %) |
| learned reader (v5) | MQuAKE | 0.313 % | 0.194 % | 0.023 % | 17.1 | 2,336 (0.06 %) |
| random reader | zsRE | 0.027 % | 0.017 % | 0.001 % | 7.0 | 225 |
| random reader | CounterFact | 2.05 % | 1.70 % | 0.52 % | 20.3 | 18,856 (0.5 %) |
| stable v0 cap | zsRE | 0.104 % | 0.034 % | 0.009 % | 27.7 | 262 |
| live v0 cap C1 | zsRE | 0.096 % | 0.046 % | 0.013 % | 27.7 | 497 |
| live v0 cap C2 | zsRE | 0.019 % | 0.016 % | 0.015 % | 50.6 | 175 |
| matched update | zsRE | 0.105 % | 0.034 % | 0.009 % | 33.8 | 280 |
| continued base (LM) + stable cap | zsRE | 0.105 % | 0.034 % | 0.010 % | 27.6 | 266 |
| every v0-family cap | CounterFact, MQuAKE | 0 | 0 | 0 | 0 | — (never fires on ordinary text) |

Three statements the figures support, and their limits:

1. **Harm is rare and concentrated for every condition that writes.** For the learned reader, between 0.16 % and
   0.31 % of positions change by more than 0.01 nats, and half of all the harm sits in 0.03–0.06 % of positions. Mean
   drift (0.002–0.007 nats) is a poor description of this: it is the average of a very small number of large losses.
2. **The learned cap and the v0-family caps have qualitatively different tails.** The learned cap disturbs more
   positions but its worst tokens are 11–17 nats; the v0-family caps (stable, live C1/C2, matched update, continued
   base) disturb fewer positions on zsRE but their worst tokens reach 28–51 nats. Live C2 is the extreme case:
   almost every position it disturbs at all is disturbed by more than 5 nats. "Rarer but heavier" versus "more
   frequent but milder" is the trade-off the survival curves show; the mean cannot distinguish them.
3. **On CounterFact and MQuAKE the v0-family caps never fire on ordinary text** (calibration radius 0: exact-prompt
   matching only), so their harm is exactly zero there, while their paraphrase retention is also zero. A cap that
   never generalises never harms; the interesting region is where retention and harm are both nonzero.

What this does not establish: a power law or any asymptotic tail class (the survival curves are empirical over a finite
population and the losses are bounded by the vocabulary), independence of positions (windows share text), robustness
to unobserved inputs, or anything about temporal clustering. The κ pilot (DEC-054) and the bounded-correction
experiment (AW-B, if run) address whether the tail can be shaped; this page only measures it.

## For the deck

Suggested placement under the heavy-tailed-distributions theme: the survival figure as the "why the mean misleads"
slide; the rarity-versus-severity figure as the comparator slide, with the sentence that the registered comparators
differ from the learned cap in the shape of the tail, not in mean drift. Numbers above are the current pooled values;
the generator reruns after the halt and the table is replaced, not edited.
