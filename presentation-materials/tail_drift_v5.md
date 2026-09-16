# Small mean drift hides large local harm — the measured tail (v5 reader, development snapshot)

Recorded 2026-09-16 for the October 15 talk ("Active Inference in the Extremes", CSS 2026 satellite).
Source of every number: Codex's HT-1b audit in the pc_cap repository at commit `2e7ac38`
(`logs/heavy_tail/audit-v5-round16/` and `…-supplement/`; task record `docs/tasks/HT-1b.md` and
`docs/tasks/HT-1b-new-results-addendum.md`). Nothing here is confirmatory: these are development cells of the
selected primary reader (primary condition v5) and of its predecessor v4, 300 edits each.

## The claim, in one sentence

After 300 edits, the cap's average preservation loss on ordinary text is a few thousandths of a nat, yet single
positions lose up to 8.7 nats: the harm is concentrated in about one position in a thousand, and the mean, the median
and even the 99th percentile do not see it.

## The numbers

Ordinary-text drift = increase in next-token negative log-likelihood (nats) of the edited model over the unedited
base, at every position of 128 shared 127-token windows (16,256 positions), original-base reference.

| statistic (positive part unless stated) | v4 · zsRE | v5 · zsRE | v5 · CounterFact |
| --- | ---: | ---: | ---: |
| signed mean, nats | +0.000233 | +0.002198 | +0.006286 |
| median | 0 | 0 | 0 |
| p95 | 0.0000079 | 0.0000080 | 0.0000082 |
| p99 | 0.0000130 | 0.0000133 | 0.0000144 |
| expected shortfall, worst 5 % | 0.00467 | 0.0440 | 0.1277 |
| maximum, nats | 3.79 | 8.69 | 7.31 |
| worst position | window 125, pos 26 | window 16, pos 31 | window 17, pos 117 |
| positions > 0.01 / > 0.1 / > 1 nat | 1 / 1 / 1 | 17 / 17 / 10 | 55 / 52 / 29 |
| share of positive harm in the worst 1 % of positions | 99.45 % | 99.94 % | 99.98 % |
| positions with exactly zero change | 4,095 | 4,090 | 4,085 |

Reading: p99 barely moves between v4 and v5 (13.0 → 13.3 micro-nats) while the mean rises tenfold and the maximum
more than doubles, because 17 positions are 0.105 % of the population and sit above p99. The v5 zsRE and CounterFact
cells put 99.9 % of all positive harm in 1 % of positions.

## The figure

`figures/mean_vs_tail_v5.{pdf,svg,png}` (Codex, `scripts/ht1b_plot_v5.py`; png sha256 `08ed50f5b0a2…`).
Left panel: signed mean, worst-5 % mean and maximum on a log scale for the three cells — the mean and the maximum
are three to four orders of magnitude apart. Right panel: empirical upper tail, the fraction of positions whose harm
exceeds x nats, as a step function with no fitted distribution; v5 zsRE reaches 8.7 nats at 1/16,256, CounterFact
7.3 nats.

## How to say it honestly

- These are descriptive comparisons of three cells with different readers and edit histories (v4 vs v5; zsRE vs
  CounterFact), on the same text and the same reference NLL vectors. They are not isolated treatment effects.
- The tail is observed concentration; nothing identifies a power law or any parametric family. Say "heavy-tailed in
  the empirical sense: the top 1 % carries 99.9 % of the harm", not "power-law".
- Positions within a window are dependent (one continuation), so the 16,256 are not independent samples.
- The 32-window short assays used during reader selection report means only (+0.0054 / +0.0137 / +0.0040 nats for
  zsRE / CounterFact / MQuAKE); they carry no per-position outcomes, so no tail can be reconstructed from them.
  The full 128-window assay is the only source of tail numbers so far.
- The v5 full and incremental driver profiles are the same run repeated, not independent replications.
- Mean drift being below a ceiling (the protocol's fidelity gate) is not a bound on maximum local harm; the talk's
  point is exactly that the gate has to be stated in tail terms (expected shortfall, exceedance counts, worst
  location) as well as in mean terms.

## What this is evidence for in the talk

The active-inference framing: an agent that assesses its own memory edits by average surprise will approve edits
that occasionally destroy a specific prediction by 7–9 nats (a probability ratio of e^8 ≈ 3,000×). The confirmatory
matrix (360 cells, 100 / 300 / 1,000 edits, three datasets, eight conditions) will report the same tail statistics
per cell; the loss-level κ (coupled-logarithm) pilot, if approved (lead decision Q4), tests whether training the
reader against a heavier-tailed surprise reduces the exceedances rather than the mean.

## Reproduction

From pc_cap: `python3 -B -m scripts.ht1b_v5_audit --output logs/heavy_tail/NEW_DIR` (CPU only, no model
loaded; refuses to overwrite). The supplement adds the CounterFact checkpoint paths to the script's `PATTERNS`.
Audit hashes: `audit-v5-round16/audit.json` sha256 `963a50da2025cd97…`, supplement `c55377b8d07ded53…`.
