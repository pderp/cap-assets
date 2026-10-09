# Heavy tails: what the project has measured, and experiments that would actually test for them

Prepared for charlie by Capstan, 2026-10-09. Part A says what "heavy-tailed" means operationally and why it is hard to
establish from data. Part B records what this project already did (HT-13, HT-15, HT-17) and where it stops. Part C
proposes experiments inside the project, ordered by what they cost; most of the first group can be run on CPU from the
saved per-position vectors and checkpoint files without touching a model. Part D is the general protocol for testing
heavy tails in any system. Nothing here is scheduled: the experimental programme is frozen as of today, and everything
in Part C is post-conference work. Sources: `docs/additional_work/HT-17_report.md`,
`docs/heavy_tail_counter_review.md`, `docs/friday-10.02-review/feedback-MMK-nelson-entropy.md` (with Capex's
corrections), `docs/presentation/qa.md` §17, §21–24, and `assets/presentation-materials/tails_v1.md`.

## Part A. What the claim means and why it resists proof

A distribution is **heavy-tailed** when its tail decays more slowly than any exponential: P(X > x) · e^{λx} → ∞ for
every λ > 0. Inside that broad class there is a hierarchy that matters for what one can claim:

| Class | Tail behaviour | Consequence | Example |
| --- | --- | --- | --- |
| Light (exponential family) | P(X > x) ≈ e^{−x/σ} | all moments finite; maxima grow like log n; averages are trustworthy | Gaussian, exponential |
| Subexponential, finite moments | slower than exponential but moments exist | the largest observation dominates sums; averages converge slowly | lognormal, stretched exponential (Weibull with shape < 1) |
| Regularly varying (power law) with tail index α | P(X > x) ≈ x^{−α} | moments of order ≥ α are infinite; for α < 2 the variance is infinite and the central limit theorem fails | Pareto, Student-t, generalised Pareto with shape ξ = 1/α > 0 |
| Bounded (compact support) | P(X > x) = 0 beyond an endpoint | a hard ceiling; generalised Pareto with ξ < 0 | any clipped or mixed quantity |

Nelson's framework names the same hierarchy with a coupling κ: κ = 0 is exponential, κ > 0 is power-law with exponent
−(1 + 1/κ), κ < 0 is compact support. For the one-sided, α = 1 case his coupled exponential *is* the generalised
Pareto distribution with shape ξ = κ and scale σ, so a peaks-over-threshold fit is a measurement of κ in his sense,
on the observed range.

Three facts make "is it heavy-tailed?" a hard empirical question:

1. **The classes are asymptotic.** They describe x → ∞. Any finite sample has a largest value, and on a finite range a
   lognormal, a stretched exponential, a truncated power law and a genuine power law can be indistinguishable. A
   fitted shape on an observed range is a *finite-range description*, not a class membership. (Capex's correction (1)
   and (3) in the 1 October feedback document say exactly this.)
2. **A straight line on a log–log plot proves nothing.** Many light-tailed distributions look straight over a decade or
   two, and least-squares on log-binned counts is biased. The accepted practice (Clauset, Shalizi and Newman, 2009) is
   maximum likelihood with a data-chosen lower cutoff, a goodness-of-fit bootstrap, and likelihood-ratio tests against
   named alternatives.
3. **Dependence inflates confidence.** Extreme-value theory assumes independent draws. Text positions in the same
   document, the same positions scored under five orders, and the same positions repeated across realizations are not
   independent draws. Intervals computed as if they were are too narrow by an unknown factor (Capex's correction (6)).

So the honest form of a heavy-tail finding is: *on this range, with this dependence structure handled this way, model
M describes held-out extremes better than model M′ by this much, with this uncertainty.* That is the form every
proposal below takes.

## Part B. What this project has already measured

The quantity is harm: Δ = NLL with cap − NLL with cap off, per token, at the same prefix, on 245,237 ordinary-text
positions (1,931 reset-context windows of 127 scored positions each), for every receipted cell.

What was done (HT-13/15 descriptive, HT-17 fitted, 303 cells):

- Empirical survival curves P(Δ > x) per condition and dataset; exceedance fractions at 0.01, 0.1, 1 and 5 nats; the
  maximum; ES99+ (mean of the worst 1 %); and "half of all harm sits in k positions".
- Peaks-over-threshold generalised-Pareto fits to excesses Δ − u at u = 0.01, 0.1, 0.5, 1 nat, with a screen of at
  least 100 excesses in at least 30 distinct windows before any shape is reported.
- Window-block bootstrap (resampling whole 127-position windows, identical multiplicities across paired conditions)
  for intervals; five-fold held-out-window log-likelihood comparison of the generalised Pareto against the exponential.
- Paired contrasts (mixture vs original; ePC vs BP reader) with the same window identities on both sides.

What it found, in one paragraph: harm is rare (0.03 to 0.3 % of positions above 0.01 nat for the learned and v0 caps;
2 % for the random reader on CounterFact) and concentrated (half of the learned reader's harm in 0.03–0.06 % of
positions). Stable v0 on zsRE has a heavier-than-exponential fitted tail at the primary threshold (shape 0.43 to 1.03
across fifteen cells, better held-out likelihood than exponential in every cell). The learned reader's fitted shapes
have intervals that include zero: an exponential describes its tail about as well. The random reader's negative fitted
shapes are untrustworthy (ten of fifteen held-out comparisons fail at a fitted endpoint). The one-nat mixture produces
fits that all hit an endpoint pathology, which is what a hard ceiling should do, and the ceiling holds regardless.

Where it stops, stated by the record itself (`qa.md` §17, §21, §24): no asymptotic tail class; no power law; no
infinite variance; no entropy growth W(N), because no system-size axis N was defined; one model scale; one text
sample reused in every cell; dependent orders; at u = 1 nat most cells fall below the sample-size screen, so the far
tail is unmeasured.

## Part C. Proposed experiments inside the project

Each entry gives the question, the design, the pre-registered decision rule, what it can and cannot show, and the cost.
"CPU, saved data" means it needs only the saved per-position vectors (`full-validation-*.npz`) and the pipeline in
`aw/` (HT-17's fitter with its 21 tests). "GPU" means new forward passes through GPT-2.

### Group 1: from saved data, no model execution

**C1. Calibrate the pipeline with synthetic positive and negative controls.**
*Question.* At our sample sizes and with our dependence structure, how often does the pipeline report a positive
shape when the truth is exponential, and how often does it miss a true shape of 0.3 or 0.6?
*Design.* Take the real zero/non-zero pattern of a learned-reader cell (which positions are harmed, in which windows),
and replace the harmful magnitudes with draws from (a) exponential, (b) generalised Pareto with ξ ∈ {0.1, 0.3, 0.6},
(c) lognormal, (d) a hard-clipped exponential, preserving within-window clustering by drawing each window's excesses
with a shared latent scale. Run the full HT-17 pipeline on each, 200 replicates per truth.
*Rule.* Report false-positive rate at the 95 % interval level and power against each alternative. Any later claim
about a real cell's shape is qualified by these rates.
*Shows.* Whether the project's instrument can see what it claims to see. *Cannot show.* Anything about the real tail.
*Cost.* CPU hours. This is the first thing to do, and arguably should have preceded HT-17's headline sentences.

**C2. Threshold stability and mean-excess diagnostics.**
*Question.* Is the fitted shape stable as the threshold u rises, as a genuine generalised-Pareto tail requires?
*Design.* For each cell with enough excesses, fit at a dense grid of u between 0.01 and the largest u that passes the
screen; plot shape and the modified scale σ_u − ξu against u with simultaneous window-bootstrap bands; plot the mean
excess e(u) = E[Δ − u | Δ > u], which is linear in u with slope ξ/(1 − ξ) under the generalised Pareto.
*Rule.* A cell "supports a stable shape" only if the shape band contains one constant across at least one decade of u.
Stable v0's reported fall in shape from 0.8 to 0.16 across thresholds is already evidence against a single power-law
body; this test makes that systematic.
*Shows.* Whether the tail is one family or a mixture. *Cost.* CPU.

**C3. Decompose frequency and severity by gate state.**
*Question.* Is the heavy tail a property of *how hard* the cap hits when it fires, or of *how often* it fires?
*Design.* The gate's firing decisions per position are saved separately from Δ (firings and Δ > 0.01 differ: 18 vs 15
in one seed). Fit the severity distribution conditional on firing, and model the firing process (rate, clustering) on
its own. Compare the tail of severity-given-firing across conditions.
*Rule.* Pre-register that the learned reader's severity-given-firing shape and v0's are compared with paired windows;
report the difference with its interval.
*Shows.* Which mechanism to target: the gate (frequency) or the write size (severity). *Cost.* CPU.

**C4. Block maxima and consistency with peaks-over-threshold.**
*Question.* Does an independent extreme-value method agree with the threshold fits?
*Design.* Take the maximum Δ in each of the 1,931 windows; fit a generalised extreme-value distribution; its shape
should agree with the generalised-Pareto shape if both are measuring the same tail. Also compute the extremal index θ
(runs or intervals estimator) to measure clustering of exceedances within windows.
*Rule.* Agreement within the joint bootstrap band counts as consistency; θ well below 1 means exceedances cluster and
the effective sample is smaller than the count of exceedances.
*Shows.* Robustness of the shape to method; the degree of temporal clustering ("temporal concentration" axis of the
counter-review). *Cost.* CPU.

**C5. A system-size axis from the checkpoints that already exist.**
*Question.* Does the tail get heavier as the memory grows? This is the nearest thing the project can offer to the
W(N) growth that Nelson's classes are about.
*Design.* Every 1,000-edit cell has saved states at 100, 300 and 1,000 edits. Run the harm assay on all three for a
fixed set of cells (three realizations × one order × two datasets × two conditions = 12 cells, 36 assays), then fit
shape, ES99+, maximum and exceedance fraction as functions of N = number of records.
*Rule.* Pre-register the direction: if the shape or ES99+ increases monotonically with N in both conditions, memory
size is a driver; if frequency grows but shape is flat, harm scales by count, not by severity.
*Shows.* The first N-dependence curve. *Cannot show.* The asymptotic growth law. *Cost.* GPU for the 100 and 300
assays (the 1,000 ones exist); roughly 24 harm assays.

**C6. Tail under known interventions as a positive control.**
*Question.* Does the fitter recover a known endpoint when one is imposed?
*Design.* The mixture guarantees Δ ≤ 1 nat exactly. Fit the mixture cells' excesses with a bounded family (ξ < 0) and
check that the estimated endpoint σ/|ξ| + u lands at 1.00 within its interval. Do the same for the clip-at-4-nat
control from AW-B.
*Rule.* Recovery of the known endpoint within the interval in all ten memories is a pass for the pipeline; failure
means endpoint estimates elsewhere (the random reader's negative shapes) must not be reported.
*Shows.* Whether negative-shape results anywhere in the project can be believed. *Cost.* CPU.

**C7. Stratify harm by input rarity.**
*Question.* The abstract says the prior is "fragile in the extremes". Is harm heavier where the base itself is
surprised?
*Design.* The cap-off NLL per position is saved. Bin positions by base NLL (deciles), by document, and by token
frequency; fit the harm tail within bins; test whether shape or exceedance frequency rises with base surprisal.
*Rule.* Pre-register a monotone trend test across deciles with window-block bootstrap.
*Shows.* Whether "extreme input" and "extreme harm" coincide, which the abstract assumes. *Cost.* CPU.

### Group 2: new forward passes, post-conference

**C8. Fresh, disjoint text.**
*Question.* Do the fitted shapes replicate on text never used in any cell?
*Design.* Draw 2,000 new OpenWebText documents disjoint from the 1,931 windows; score the saved end-of-stream
checkpoints of a pre-registered set of cells (say the fifteen learned-reader and fifteen v0 cells on zsRE); treat
documents, not windows, as the blocks.
*Rule.* Replication means the new shape interval overlaps the old one and the held-out exponential comparison has the
same sign.
*Shows.* Whether the HT-17 shapes are a property of the cap or of the particular text sample. This is the single most
important test, because the same text was reused 303 times. *Cost.* One harm assay per cell: about 30 GPU assays.

**C9. Base-scale series.**
*Question.* Does the harm tail change with the size of the frozen prior?
*Design.* Same cap recipe on GPT-2 medium (355M, 24 blocks; sites at 8, 16, 24 by the same rule) and, if affordable,
GPT-2 large. One realization, one order, both datasets, the learned reader only; the JAX port is the same code with a
different configuration.
*Rule.* Pre-register whether shape, frequency and ES99+ are compared at matched retention or at matched edits.
*Shows.* Whether "transfer to production scale is not established" can start to be addressed. *Cost.* Reader retraining
per base plus two 1,000-edit cells per base; days of local GPU.

**C10. Credit rule and the tail, pre-registered.**
*Question.* Does the error-inference credit change the tail of harm, not just its mean?
*Design.* HT-17 already paired ePC and BP readers by window. Extend to the fixed-v5 credit cells and the settling-depth
series (1, 8, 32 steps) with the same window bootstrap, and pre-register a one-sided test on ES99+ and on the shape.
*Rule.* A difference counts only if its paired interval excludes zero and the synthetic control (C1) shows power to
detect that size.
*Shows.* Whether the deck's "largest token loss 9.26 vs 12.27 nats" is a tail effect or noise. *Cost.* CPU if the
vectors exist (they do for the four fixed-v5 cells and the depth controls); GPU for any new cell.

**C11. Memory pressure and near-collision density.**
*Question.* Does the tail thicken as records crowd the key space?
*Design.* Use realization 3's extra subjects (Option R) and construct streams where facts about neighbouring subjects
are deliberately dense versus sparse; measure near-miss false fires and the harm tail at matched N.
*Shows.* The "memory pressure" and "boundary failure" axes of extremeness. *Cost.* GPU, a handful of cells.

**C12. A real κ axis.**
*Question.* The one-κ conjecture says a single coupling governs tail weight and blanket porosity. Can both be measured
on the same runs?
*Design.* Rerun the loss-level κ pilot's arms (κ = 0, 0.2, 0.5, clip control) with the full harm assay instead of the
4,064-position drift sample, so that shapes pass the screen; measure porosity as unseen-prompt false-fire rate and
tail weight as the fitted shape; pre-register that the conjecture predicts a monotone relation between the two that
the clip control does not reproduce.
*Shows.* The first test of the conjecture's prediction rather than its vocabulary. *Cost.* 9 reader trainings plus
assays; GPU days.

### Priority

| Order | Experiment | Why first |
| --- | --- | --- |
| 1 | C1 synthetic calibration | nothing else is interpretable without it |
| 2 | C6 known-endpoint control | validates or retracts every negative-shape result already published internally |
| 3 | C2, C4 stability and block maxima | cheap, and they decide whether "one family" is even the right question |
| 4 | C8 fresh text | the replication the record most lacks |
| 5 | C5 N-axis from existing checkpoints | the only route to a growth statement, and the checkpoints are already saved |
| 6 | C3, C7 decomposition and input rarity | mechanism and the abstract's premise |
| 7 | C10, C12, C9, C11 | predictive-coding, κ, scale, memory pressure |

## Part D. Testing for heavy tails in general

The same logic applies to request latencies, financial returns, neural avalanches, earthquake magnitudes, city sizes,
or per-token losses of any model. A defensible protocol has eight parts.

**1. Define the variable, the unit, and the sampling frame before looking.** State what is measured (a loss, a
magnitude, a duration), its units, the population of events, and what counts as one observation. Changing the
reference measure changes the tail (a log-transformed variable has a different class); say which one is meant.

**2. Decide the dependence structure first.** Identify the natural blocks (documents, days, trials, subjects). All
resampling and all held-out evaluation operate on blocks. Estimate the extremal index to learn how many effectively
independent extremes there are; if it is far below one, decluster (take one extreme per cluster) before fitting.

**3. Collect enough extremes.** Rules of thumb: at least 100 exceedances above the threshold, spread over at least 30
blocks, before reporting a shape; at least an order of magnitude of range above the threshold before discussing a
class. Below that, report frequencies and conditional means, not shapes.

**4. Describe before fitting.** Empirical survival on log–log axes (for the eye only), the mean-excess plot, Hill and
moment-estimator plots against the number of order statistics, the maximum-to-sum ratio M_n/S_n for the first few
moments (it tends to zero if that moment is finite, and stays away from zero if not), and the share of the total
carried by the top 1 % and 0.1 %. These are diagnostics, not evidence.

**5. Fit by likelihood with a data-chosen threshold and compare against named alternatives.** Two complementary
routes:
- *Peaks over threshold*: generalised Pareto on excesses; choose the threshold by minimising a goodness-of-fit
  distance or by the stability plots; report shape, scale and the threshold together. Shape ξ > 0 is heavy, ξ = 0
  exponential, ξ < 0 bounded. In Nelson's notation ξ is κ and the scale is the informational scale σ.
- *Block maxima*: generalised extreme-value on per-block maxima; its shape should agree with the threshold fit.
Then the Clauset–Shalizi–Newman discipline: a bootstrap goodness-of-fit p-value for the chosen family, and
likelihood-ratio tests (Vuong) against lognormal, exponential, stretched exponential and power law with exponential
cutoff. A power law that is not favoured over a lognormal on the observed range should be reported as "not
distinguishable from lognormal", not as a power law.

**6. Validate on held-out extremes.** Split by blocks; fit on some, score the largest held-out observations under
each candidate; the family with the better held-out log-likelihood on the extremes wins for that range. An estimated
endpoint that excludes a held-out observation falsifies the bounded fit outright. Report every failure, do not drop it.

**7. Calibrate the instrument.** Simulate from known families with the real block structure and the real sample size;
report the pipeline's false-positive rate and power. State the smallest shape it could have detected.

**8. Put the asymptotics where they belong.** A finite-range shape is a measurement; "heavy-tailed" as a class is an
extrapolation. To make a class claim, one needs a system-size axis N and a demonstration that the shape, or the growth
of the number of accessible states, follows the claimed law across N. In physical systems that is the scaling study
(system size, time window, population). In a learning system it can be memory size, model size, stream length or
dataset size, and the right statement is "the shape at N = … is …, and across N it behaves as …".

Three experimental designs that are worth stating generally, because they turn description into a test:

- **Intervention with a known tail.** Impose a bound (a clip, a mixture, a cap) whose effect on the tail is known
  exactly, and confirm that the fitted family recovers it. If the pipeline cannot find a ceiling it was given, it
  cannot be trusted to find a power law it was not.
- **Scale series.** Repeat the measurement at three or more sizes along the most plausible N and fit shape against N
  with the same block bootstrap. One size tells you nothing about a class.
- **Replication on a disjoint sample.** A tail found once on one sample, however large, is a hypothesis; the same
  shape on an independent sample under a pre-registered rule is a result.

## One paragraph for a questioner

We measured the distribution of unintended per-token harm on 245,237 positions for 303 cells; it is rare and
concentrated, and the fitted generalised-Pareto shapes differ between cap designs on the observed range, with stable
v0 heavier than exponential and the learned reader indistinguishable from exponential. We claim no asymptotic class,
because the text sample was reused, the orders are dependent, there is no system-size axis, and the far tail falls
below our sample-size screen. The experiments that would move this from description to test are, in order: calibrate
the fitting pipeline on synthetic truths with our block structure, confirm it recovers the one-nat ceiling we imposed,
replicate the shapes on disjoint text, and measure shape against memory size using the checkpoints we already have.
