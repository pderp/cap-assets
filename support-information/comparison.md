# No cap versus the cap: results on all three datasets

Capstan · 9 October 2026 · every number below is read from the frozen record in `pc_cap`; sources are listed at the end.

## 1. What "no cap" means and how it was measured

"No cap" is the frozen GPT-2 small (124M parameters) answering on its own. In the code this is the cap-off path: the same forward pass with a zero write at every site, which reproduces the base bit for bit.

Three things follow from that, and the record confirms them where it measured them:

- **Edit metrics are zero.** Every dataset asks the base to produce an answer it does not already give (CounterFact and MQuAKE targets are counterfactual by construction; the zsRE items used here are ones the base misses). The AW-B study scored an explicit cap-off arm on the 300-edit development memories for zsRE and CounterFact: edit success 0, own-prompt retention 0, paraphrase retention 0. MQuAKE has no separately scored cap-off arm; the same zero holds by construction.
- **Preservation metrics are perfect.** Locality and near-miss ask whether an unrelated prompt still gives the base's answer. With no cap it is the base's answer, so both score 100 %. The cap-off arm measured 1.0 on both.
- **Harm is zero at every position.** Harm is defined as Δ = loss with cap − loss without cap. With no cap, Δ = 0 for all 245,237 positions, so mean KL, ES99+ and the maximum are all 0. The cap-off arm measured exactly that.

So the no-cap column is the fixed point every cap is measured against: it edits nothing and damages nothing. The question each cap answers is how much editing it buys for how much damage.

## 2. Main comparison: the confirmatory study, GPT-2 small

Three subject realizations, five orders each, 1,000 edits (300 for MQuAKE). Scores are averaged over orders within each realization, then across the three realizations, exactly as on the deck's results slide. "Learned reader" is the selected v5 reader with adjoint credit; "Stable v0" is the first-generation radius-gated cap; "Random reader" is the untrained-reader control.

### 2.1 Editing and preservation (percent)

| Dataset | Condition | Edit success | Own-prompt retention | Paraphrase retention (primary) | Locality | Near-miss |
|---|---|---:|---:|---:|---:|---:|
| zsRE, 1,000 edits | No cap | 0 | 0 | 0 | 100 | 100 |
| | Stable v0 | 99.99 | 66.68 | 18.56 | 97.07 | 32.40 |
| | Random reader | 100 | 100 | 52.40 | 99.33 | 0 |
| | **Learned reader (v5)** | 99.44 | 98.23 | **96.03** | 100 | 88.33 |
| CounterFact, 1,000 edits | No cap | 0 | 0 | 0 | 100 | 100 |
| | Stable v0 | 100 | 100 | 0 | 100 | 100 |
| | Random reader | 100 | 100 | 12.05 | 0.67 | 0 |
| | **Learned reader (v5)** | 99.29 | 97.70 | **67.80** | 98.67 | 100 |
| MQuAKE, 300 edits | No cap | 0 | 0 | 0 | 100 | 100 |
| | Stable v0 | 100 | 100 | 0 | 100 | 100 |
| | Random reader | 100 | 100 | 0 | 0 | 0 |
| | **Learned reader (v5)** | 100 | 99.89 | **71.56** | 100 | 100 |

Edit success: the target answer appears immediately after teaching. Own-prompt retention: the original prompt still gives the taught answer at the end of the run. Paraphrase retention: a held-out rewording gives the taught answer at the end. Locality: 200 unrelated prompts still give the base's complete answer. Near-miss: prompts about a neighbouring fact still give the base's answer.

### 2.2 Harm on ordinary text (245,237 OpenWebText positions, nats)

| Dataset | Condition | Mean KL per token | Harmful-change frequency (Δ > 0.01) | Conditional severity | Mean cell ES99+ | Mean per-cell max | Max across cells |
|---|---|---:|---:|---:|---:|---:|---:|
| zsRE | No cap | 0 | 0 % | — | 0 | 0 | 0 |
| | Stable v0 | 0.0016 | 0.104 % | 1.716 | 0.179 | 25.31 | 27.68 |
| | Random reader | 0.0005 | 0.027 % | 1.806 | 0.048 | 6.16 | 7.00 |
| | Learned reader (v5) | 0.0024 | 0.159 % | 1.630 | 0.260 | 9.75 | 11.05 |
| CounterFact | No cap | 0 | 0 % | — | 0 | 0 | 0 |
| | Stable v0 | 0 | 0 % observed | undefined | 0 | 0 | 0 |
| | Random reader | 0.0711 | 2.045 % | 3.486 | 5.454 | 18.01 | 20.28 |
| | Learned reader (v5) | 0.0054 | 0.298 % | 1.913 | 0.571 | 13.59 | 15.38 |
| MQuAKE | No cap | 0 | 0 % | — | 0 | n/a | n/a |
| | Stable v0 | 0 | n/r | n/r | n/r | 0 | n/r |
| | Random reader | 0.0122 | n/r | n/r | n/r | 14.24 | n/r |
| | Learned reader (v5) | 0.0061 | n/r | n/r | n/r | 13.49 | n/r |

Mean KL and mean per-cell max come from the confirmatory summary (same averaging as table 2.1). Frequency, severity, ES99+ and max across cells come from HT-17, which fitted the zsRE and CounterFact Stage-4 cells only; "n/r" means not reported in that study for MQuAKE. ES99+ is the mean Δ over the worst 1 % of positions. The registered preservation benchmark was mean KL ≤ 0.001; the learned reader exceeded it in all 45 cells.

### 2.3 How to read the three columns together

- **No cap** is the zero point: no edits, no damage.
- **Stable v0** on CounterFact and MQuAKE is indistinguishable from no cap on ordinary text (it never fires there) and perfect on the original prompt, but it has 0 % paraphrase generalization. On zsRE it fires more, retains less, and carries the largest single-position harm in the study.
- **The learned reader** is the only condition that generalizes to paraphrases on all three datasets. It pays for that with mean KL of 2 to 6 thousandths of a nat, harm on 0.16 to 0.30 % of positions, and worst positions of 10 to 15 nats.
- **The random reader** shows what the gate alone buys without training: much lower paraphrase retention and, on CounterFact and MQuAKE, locality collapses because it fires on almost everything.

## 3. Predictive coding inside the cap

Two places in the project use predictive coding on GPT-2 small, and each was compared against its backprop twin. There is no "no cap" row in these tables because the comparison is between two caps; the no-cap row would be the same zeros as above.

### 3.1 Acquisition credit: adjoint versus error inference (PC-v1)

Frozen GPT-2 small, the fixed v5 reader, 300 edits, one realization (0), order 100. Only the direction used to teach each write changes: ordinary backprop through the frozen base, or eight settling steps of error inference.

| Dataset | Credit | Paraphrase retention | Own-prompt retention | Locality | Harm frequency (Δ > 0.01) | Mean Δ per token | ES99+ | Max token loss | Acquisition process time |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| zsRE | Adjoint | 98.3 % | 100 % | 100 % | 0.118 % | 0.0018 | 0.196 | 9.26 | 312 s |
| zsRE | Error inference | 98.3 % | 100 % | 100 % | 0.118 % | 0.0017 | 0.182 | 12.27 | 422 s |
| CounterFact | Adjoint | 80.7 % | 100 % | 100 % | 0.282 % | 0.0044 | 0.459 | 11.74 | 293 s |
| CounterFact | Error inference | 80.3 % | 100 % | 100 % | 0.285 % | 0.0045 | 0.470 | 12.23 | 355 s |

Endpoints are nearly identical; the error-inference arm costs about 35 % more acquisition time and has a higher single-position maximum on both datasets. One realization only, so this is a transfer check, not an interval.

### 3.2 Training the reader: backprop versus error predictive coding (PC-reader)

Three paired seeds, 300 updates, 3,348,228 reader parameters, GPT-2 small. Evaluation uses adjoint acquisition and 300 edits.

| Dataset | Seed | BP paraphrase retention | ePC paraphrase retention | BP training time | ePC training time |
|---|---:|---:|---:|---:|---:|
| zsRE | 0 | 97.3 % | 94.7 % | 0.24 h | 24.6 h |
| zsRE | 1 | 99.0 % | 97.0 % | 0.25 h | 24.1 h |
| zsRE | 2 | 97.7 % | 98.0 % | 0.24 h | 23.4 h |
| CounterFact | 0 | 81.0 % | 56.8 % | (same reader) | (same reader) |
| CounterFact | 1 | 80.0 % | 77.8 % | | |
| CounterFact | 2 | 83.5 % | 66.0 % | | |

Own-prompt retention is 99 to 100 % in every cell for both rules. ePC training took 96 to 102 times the backprop time and lost paraphrase retention on CounterFact in all three seeds.

### 3.3 Settling depth on the 50M ePC base (PC-v0 depth controls)

This is the slide "More settling bought retention at a cost". It does **not** use GPT-2 small: the base is the regenerated 50M-parameter ePC checkpoint, with the stable v0 cap, zsRE, three exposed realizations, order 100, 1,000 edits. It is listed here so the comparison is complete, but its numbers must not be placed in the GPT-2 tables above.

| Settling steps | Own-prompt retention | Paraphrase retention | Locality | Mean KL | Largest single max | Learning time |
|---:|---:|---:|---:|---:|---:|---:|
| 1 (= adjoint) | 51.5 % | 13.1 % | 97.0 % | 0.0018 | 5.47 | 276 s |
| 8 | 53.4 % | 13.1 % | 97.7 % | 0.0022 | 3.25 | 614 s |
| 32 | 56.5 % | 12.2 % | 99.7 % | 0.0026 | 8.03 | 1,525 s |

On CounterFact at every depth the v0 cap never fired on ordinary text and scored 100 / 100 / 0 (edit, own-prompt, paraphrase), identical across settling depths.

## 4. The bounded correction (mixture) against both references

AW-B, ten exposed 300-edit development memories (five orders per dataset), GPT-2 small, v5 reader. The mixture keeps ρ = e⁻¹ ≈ 0.37 of the base's next-token distribution.

| Dataset | Arm | Paraphrase retention | Own-prompt retention | Mean KL | ES99+ | Max token loss | Conditional severity (Δ > 0.01) |
|---|---|---:|---:|---:|---:|---:|---:|
| zsRE | No cap | 0 % | 0 % | 0 | 0 | 0 | — |
| zsRE | v5 cap | 97.3 % | 99.7 % | 0.00227 | 0.237 | 9.94 | 1.619 |
| zsRE | v5 cap + mixture | 97.3 % | 99.7 % | 0.00071 | 0.076 | 1.00 | 0.542 |
| CounterFact | No cap | 0 % | 0 % | 0 | 0 | 0 | — |
| CounterFact | v5 cap | 75.3 % | 100 % | 0.00593 | 0.610 | 14.02 | 1.925 |
| CounterFact | v5 cap + mixture | 74.5 % | 100 % | 0.00160 | 0.173 | 1.00 | 0.581 |

The mixture is the one intervention that moves the cap part of the way back toward the no-cap column on harm (mean KL and ES99+ cut 3.2 to 3.5 times, worst token capped at one nat) while leaving the edit endpoints essentially where they were. It does not reach the registered 0.001 mean-KL benchmark on CounterFact.

## 5. One-paragraph version

With no cap, GPT-2 small edits nothing and is damaged nowhere. The learned-reader cap retains 96 % of taught paraphrases on zsRE, 68 % on CounterFact and 72 % on MQuAKE after 1,000 (300) edits, keeps locality at 99 to 100 %, and costs 2 to 6 thousandths of a nat of mean KL on ordinary text, with harm concentrated on 0.16 to 0.30 % of positions and worst single tokens of 10 to 15 nats. Stable v0 sits between the two on CounterFact and MQuAKE (perfect own-prompt memory, zero paraphrase generalization, zero ordinary-text harm) and is worse than the learned reader on every axis on zsRE. Swapping backprop for predictive coding inside the cap, either as the teaching direction or as the reader's training rule, did not improve any of these numbers on GPT-2 small; it matched them at higher cost in the first case and lost paraphrase retention at 100 times the cost in the second.

## Sources

- Confirmatory summary (tables 2.1, 2.2 mean KL and per-cell max): `pc_cap/logs/R1/reports/triplet/summary.json`, groups for `R1_learned_ff`, `v0_stable`, `R1_nonlearned` at checkpoint 1000 (300 for MQuAKE), fields `primary`, `near_miss`, `fidelity.capoff`.
- Harm frequency, severity, ES99+, max across cells: `pc_cap/docs/additional_work/HT-17_report.md`, table "Frequency and severity are different questions".
- Cap-off (no cap) measured row and mixture (table 4): `pc_cap/docs/additional_work/AW-B_report.md`, settings `capoff`, `v5`, `mixture:0.367879`; severities from `pc_cap/docs/presentation/numbers_to_say.md` [H].
- PC-v1 credit arms (table 3.1): `pc_cap/results/additional_work/PC-v1/replication-4-20260927/*/checkpoint-300.json` and `finish.json`; harm from `pc_cap/logs/additional_work/PC-v1/report-4-20260927/harm/report.json`.
- PC-reader (table 3.2): `pc_cap/docs/additional_work/PC-reader_report.md`.
- Depth controls on the 50M ePC base (table 3.3): `pc_cap/logs/additional_work/PC-v0/controls-report-20260929/report.json`, `summary`; base identity in `pc_cap/docs/additional_work/PC-v0.md`.
- Deck: `Predictive_Coding_Cap_Experiments.pdf` (26-slide export), slides "What we measure", the results table slide, "Frozen GPT-2 and the selected v5 reader", "Training the reader with predictive coding", "The probability mixture", "More settling bought retention at a cost".
