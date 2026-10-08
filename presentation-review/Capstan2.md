# Capstan review, round 2 (2026-10-08, export of 09:58)

Checked the new export against the previous one (text diff) and against the record. Section 1 covers your corrections; section 2 is the slide 15 table to paste.

## 1. Your corrections, checked

| Item | Status in the 09:58 export | Notes |
|---|---|---|
| 1.1 CounterFact link | fixed | Now arXiv 2202.05262 (Meng et al. 2022). Verified in the PDF's link table. |
| 1.2 Slide 7 | fixed | Text matches `slide7.md` and fits the slide. |
| 1.3 Slide 6 | fixed | Clause added. The last sentence has no full stop ("... not a local hardware rule"). |
| 1.4 Slide 18 | **unchanged** | The export still reads "An adjoint control used 53–58% of its offered budget. Credit direction versus actual compute remains unresolved." If that is deliberate, fine; if not, the rewrite from `Capstan.md` §1.4 is still the one I recommend. It is the one slide a listener cannot follow without the setup. |
| 1.5 Title | fixed | Slide 3 now carries the submitted title; slide 1 names the satellite. Two small things: slide 1 is missing the space after the colon ("satellite:Thriving"), and the word "presentation" at the end is redundant. Suggest "CSS2026 satellite: Thriving in the Extremes". On slide 3, "Original plan, submitted as: ..." reads as if the plan was submitted; "Original plan. Talk submitted as: ..." avoids that. |
| 2, slide 11 | fixed | "One realization shown below." added. |
| 2, slide 15 | caption fixed, table pending | "The cost is both in time and harm." is now in the caption but the table does not yet show harm. Table below. |
| Slide 23 | new | The FabricPC link (github.com/trueagi-io/FabricPC) resolves. "Our FabricPC library for predictive coding was utilized with this work" is accurate. |

No number changed between the two exports; everything verified in `Capstan.md` §2 still holds.

## 2. Slide 15: replacement table

All values are from the PC-v0 settling-depth controls report (`pc_cap/docs/additional_work/PC-controls_report.md`, means over the three realizations, zsRE, order 100, 1,000 edits). Harm columns are measured on 245,237 positions of ordinary text as the per-token loss increase Δ = loss with cap − loss without cap, in nats. "Worst 1%" is ES99+, the mean of Δ over the worst 1% of positions. The adjoint arm does not settle; its three depth-paired runs are within rounding of each other (learning time 4.6–4.7 min), so one reference row suffices.

### Recommended (one adjoint reference row)

| Credit | Settling steps | Original-prompt retention | Paraphrase retention | Mean loss increase, ordinary text | Worst 1% of positions (ES99+) | Learning time per cell |
|---|---|---|---|---|---|---|
| Adjoint (reference) | none | 51.5% | 13.1% | 0.00145 nats | 0.156 nats | 4.6 min |
| Error inference | 1 | 51.5% | 13.1% | 0.00145 nats | 0.156 nats | 5.7 min |
| Error inference | 8 | 53.4% | 13.1% | 0.00157 nats | 0.167 nats | 10.2 min |
| Error inference | 32 | 56.5% | 12.2% | 0.00221 nats | 0.236 nats | 25.4 min |

Tab-separated for pasting (paste into a Google Sheet first, then copy the range into the slide; Slides keeps the grid that way):

```
Credit	Settling steps	Original-prompt retention	Paraphrase retention	Mean loss increase, ordinary text	Worst 1% of positions (ES99+)	Learning time per cell
Adjoint (reference)	none	51.5%	13.1%	0.00145 nats	0.156 nats	4.6 min
Error inference	1	51.5%	13.1%	0.00145 nats	0.156 nats	5.7 min
Error inference	8	53.4%	13.1%	0.00157 nats	0.167 nats	10.2 min
Error inference	32	56.5%	12.2%	0.00221 nats	0.236 nats	25.4 min
```

### Suggested caption (replaces the current one)

> Legacy 50M ePC base with the v0 live cap: zsRE, three exposed realizations, order 100, after 1,000 edits. Harm is the per-token loss increase on 245k positions of ordinary text. One step of error credit is algebraically the adjoint direction; the cost of deeper settling is in time and in harm.

### What the table shows (for the spoken line)

- Own-prompt retention rises with depth (51.5 → 53.4 → 56.5%), paraphrase retention does not (13.1 → 13.1 → 12.2%).
- Mean harm rises 8% at eight steps and 52% at 32 steps; the worst-1% mean rises by the same proportions (0.156 → 0.167 → 0.236 nats).
- Learning time rises 2.2× and 5.5× over the adjoint reference.
- Not shown, but in the report: the largest single loss increase is not monotone (5.47 nats at one step, 3.25 at eight, 8.03 at 32), so eight steps is the one depth where the worst event got smaller. Mention only if asked.

### If you prefer the full paired version

Six rows, adjoint at each depth. Only the learning-time column differs between the adjoint rows (4.6, 4.7, 4.6 min); every other adjoint value is identical to the reference row above. I would not use it on a slide; it is here for completeness.

| Credit | Settling steps | Original-prompt retention | Paraphrase retention | Mean loss increase | Worst 1% (ES99+) | Learning time per cell |
|---|---|---|---|---|---|---|
| Adjoint | 1 (paired) | 51.5% | 13.1% | 0.00145 nats | 0.156 nats | 4.6 min |
| Error inference | 1 | 51.5% | 13.1% | 0.00145 nats | 0.156 nats | 5.7 min |
| Adjoint | 8 (paired) | 51.5% | 13.1% | 0.00145 nats | 0.156 nats | 4.7 min |
| Error inference | 8 | 53.4% | 13.1% | 0.00157 nats | 0.167 nats | 10.2 min |
| Adjoint | 32 (paired) | 51.5% | 13.1% | 0.00145 nats | 0.156 nats | 4.6 min |
| Error inference | 32 | 56.5% | 12.2% | 0.00221 nats | 0.236 nats | 25.4 min |

Source rows (unrounded): RET-ES 0.515333 / 0.534 / 0.565; RET-GS 0.130667 / 0.131 / 0.122; mean ΔNLL 0.00145132 (adjoint), 0.00145136 / 0.00157227 / 0.0022107; ES99+ 0.155812 (adjoint), 0.155816 / 0.166889 / 0.23644; learning s/cell 275.934 / 280.837 / 273.309 (adjoint), 341.182 / 614.015 / 1524.85.
