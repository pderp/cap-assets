# Loss-level κ pilot — result (development, 2026-09-16)

Source: pc_cap `logs/r1_round18/ht3d-pilot-final-aliases.md` / `.json` (sha256 `c61618b7451d7414…`),
design `manifests/revision_v1/kappa_pilot_v3.json`, decision DEC-054, rule from `docs/heavy_tail_counter_review.md` §4.

## Result in one sentence

Replacing the reader's answer surprisal −ln p by the coupled logarithm −ln_κ p (κ = 0.2, 0.5) lowers the drift tail
and the false-fire rate but costs retention beyond the pre-registered floor, and a plain clipped surprisal gets most
of the same tail reduction: under the rule fixed before the runs this is a null result, and descriptively it shows
that bounding surprisal shifts the porosity / interference trade-off rather than improving it.

## The numbers (macro means over zsRE / CounterFact / MQuAKE development streams × seeds 0, 1, 2)

| arm | mean RET-GS | zsRE unseen false fires | ES95 of positive drift harm (nats) | max harm (nats) |
| --- | ---: | ---: | ---: | ---: |
| ordinary, κ = 0 (the selected v5 family) | 0.796 | 11.7 % | 0.223 | 5.26 |
| κ = 0.2 | 0.754 | 5.0 % | 0.084 | 2.70 |
| κ = 0.5 | 0.748 | 4.0 % | 0.063 | 2.60 |
| clipped surprisal, min(−ln p, 2) — control matched to κ = 0.5's ceiling | 0.779 | 4.7 % | 0.103 | 3.62 |

Pre-registered rule (counter-review §4): a κ arm becomes a declared secondary condition only if mean RET-GS drops
≤ 0.02, unseen false fires do not rise, and one tail statistic moves by more than its seed spread. Retention floor
0.776: κ 0.2 and κ 0.5 fail it. Seed-spread thresholds: ES95 0.387, max 4.44 nats (the ordinary arm's own seeds range
0.06–0.45 in ES95); the observed reductions (−0.14 / −0.16 ES95, −2.6 / −2.7 max) are inside them.

## How to say it

- "Preliminary hints" (Matthew Ikle's framing, binding by DEC-054): nine trainings, three seeds, development streams,
  a 32-window / 4,064-position tail population per dataset; no confirmatory claim.
- **What it is not.** It is not the coupled free energy of Nelson et al. (no coupled expectation, no changed
  inference distribution), not a coupled Markov blanket, and not a test of the one-κ conjecture that porosity and
  interference are the same parameter. It is the first controlled measurement of what a loss-level coupling does on
  this substrate.
- The clipped control matters: whatever the coupled form does here, a ceiling on surprisal does most of it. κ = 0.5
  minus clip-2: ES95 −0.04, max −1.0 nats, RET-GS −0.03 — small, unseparated, bought with retention.
- The direction is consistent across all three datasets and all seeds: bounded surprisal → the reader rejects more
  → fewer false fires, smaller tail, less retention. That is the trade-off slide, not an improvement slide.

## Files

`figures/` will receive the arm comparison figure when it is produced (HT-4c / slide preparation); until then the
per-arm-seed table in the source report is the figure's data.
