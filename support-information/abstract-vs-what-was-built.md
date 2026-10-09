# The abstract's non-equilibrium claims against what was built: a ledger

Prepared for charlie by Capstan, 2026-10-09. Companion to `far-from-equilibrium-and-this-project.md`. One row per idea
in the July abstract (*Coupled Active Inference on a Frozen Transformer Prior: A Risk-Aware Residual Agent for
Non-Equilibrium Regimes*, Derr and Iklé), with its status in plain words and the sentence that can be said about it
without overclaiming. Status words follow the record's convention: **built** = a working component exists in the code
that ran; **measured** = a result exists on a named population; **proposed** = in the abstract or programme, not
built. Condensed from `docs/presentation/abstract_to_testbed.md` (HT-14) and `docs/presentation/qa.md`.

## A. The architecture

| Abstract idea | Status | What exists | What it is not | What can be said |
| --- | --- | --- | --- | --- |
| A frozen pretrained transformer as the generative prior | built, measured | GPT-2 small (124M), frozen; parameter digest checked before and after every cell | not frontier scale | "The prior is frozen throughout; no base weight ever received a gradient." |
| A small adaptive agent learning only the residual R = F* − F₀ | built, measured | the cap: per-fact write vectors at three residual-stream sites, taught from the answer's prediction error; the learned reader is 3.35M parameters, 2.7 % of the base | not a general residual network trained on the whole stream; it stores per-fact corrections retrieved by a gate | "The agent learns only residual writes; the base's own function is untouched." |
| "Sparse columnar residual network" | partly built | sparse per-record memory, bank-wise writes (v0), reader plus controller (v1) | no column formation, growth policy or core–periphery scales | "A sparse record memory; the columnar organisation was not built." |
| Prior-side Markov blanket | built as an interface | read taps and bounded, reversible writes after blocks 4, 8, 12 | no conditional-independence measurement; "κ-porous" is a label | "A read/write interface to the prior with a fixed write bound; not shown to be a blanket." |
| Environment-side Markov blanket | built as an interface | the query interface with a learned null decision | no environment model; the only action is apply or withhold a correction | "A query interface with refusal; not shown to be a blanket." |
| Nested blankets (agent, column, core–periphery) | proposed | — | — | "Proposed." |

## B. The learning signal

| Abstract idea | Status | What exists | What it is not | What can be said |
| --- | --- | --- | --- | --- |
| Prediction error as the learning signal | built, measured | adjoint credit (ordinary backprop through the frozen base) and error-inference credit (settled ePC errors at the sites); the reader trained by backprop | the ePC credit is computed by autodiff through the graph, not a local hardware rule | "Every write is taught from the answer's prediction error; two credit rules were compared." |
| Predictive coding as the principled local rule | built, measured | the ePC base, the settling-depth controls, the PC-trained reader (three seeds) | one settling step equals the adjoint; eight steps gained own-prompt retention at twice the time; the matched adjoint control used only 53–58 % of its budget, so the cause is unresolved; ePC reader training cost 96–102× and lost paraphrase retention on CounterFact in all three seeds | "Predictive coding was a credit rule, tested; it did not show a clear advantage over the adjoint on this substrate." |
| Settling as a non-equilibrium process | not applicable | the settling is descent to an energy minimum with weights fixed | it is an equilibrium computation inside one edit | "The non-equilibrium content is the stream, not the settling." |

## C. Risk, tails and the extremes

| Abstract idea | Status | What exists | What it is not | What can be said |
| --- | --- | --- | --- | --- |
| Residual errors turn heavy-tailed in the extremes | measured, descriptively | 245,237-position harm vectors for 303 cells; harm rare (0.16–0.30 % of positions above 0.01 nat for the learned reader) and concentrated (half of it in 0.03–0.06 % of positions); maxima 11–17 nats; generalised-Pareto fits: stable v0 zsRE heavier than exponential (shape 0.43–1.03), learned reader near exponential (shape intervals include zero) | no asymptotic tail class, no power law, no infinite variance; dependent positions and orders; one scale | "Harm is rare and concentrated, and the two cap designs differ in fitted tail shape; we claim no tail class." |
| Risk-aware: refuse to act under low evidence | built, measured | the null decision (null mass ≥ 0.5 → no write) and the rare-token gate; false fires measured on unseen and near-miss prompts | a hard gate, not an expected-free-energy planner | "The reader refuses when no record applies; refusal errors are measured." |
| Precision kept finite on tail events; the agent persists in the extremes | partly measured, by a different mechanism | the one-nat mixture bound: no token's loss can rise by more than 1 nat; conditional severity cut about 3× (1.619 → 0.542, 1.925 → 0.581 nats); worst losses 9–15 → 1.00; editing endpoints essentially unchanged | not coupled free energy, not a precision mechanism; an analytic ceiling applied at query time | "A simple analytic bound controlled the extremes without needing to know their distribution." |
| Precision weighting as risk sensitivity | proposed | per-site error scaling exists inside the ePC solver | not used as a policy or audit weighting | "Proposed." |
| One coupling κ governs error tail-weight and blanket porosity | pilot only, null | loss-level κ pilot (κ = 0.2, 0.5): tail and false fires down, paraphrase retention below the registered floor; a clipped-surprisal control did most of the same | not Nelson's coupled free energy (no coupled expectation, no escort distribution, no changed inference distribution); the one-κ conjecture untested | "A loss-level κ pilot shifted the porosity/interference trade-off rather than improving it; it did not test the coupled theory." |
| Coupled free energy as the training objective | proposed; numerical calibration only | CAL-1: the κ-deformed one-sided family and its calibrated entropy checked by quadrature against closed forms (twelve cases, discrepancy ≤ 1.8 × 10⁻¹¹) | no training run, no agent; which random variable, which functional and how to differentiate the normalisation are undecided | "Specification work for a post-conference collaboration." |

## D. The active-inference loop

| Abstract idea | Status | What exists | What it is not | What can be said |
| --- | --- | --- | --- | --- |
| Expected-free-energy policy selection with a risk term | proposed | fixed routing rule (gate plus top-1 selection) | no preference model, no risk term, no policy search | "Not established; investigators supply the edits and the probes." |
| Epistemic value; uncertainty-triggered audits | proposed | locality, near-miss, revision and stress probes chosen by the investigators | not autonomous information seeking | "The audits found the failures that changed the design; that was us, not an agent." |
| Learning from failure ("the regime that threatens the agent carries what it can learn") | measured in one sense | the tail exists and is where the cap's errors live; the drift assay, unseen-prompt and MQuAKE null failures each changed the design | no agent uses the tail signal | "True of the programme's process; not yet of an agent." |
| Forgetting as an auditable geometric invariant | measured operationally | five orders per realization; state hashes, supersession, isolated restores; v0 order-reversal damage measurements | no holonomy or geometric computation | "Interference is measured as order dependence; no geometric claim." |

## E. The satellite's own objectives

| Objective | Our evidence | Limit |
| --- | --- | --- |
| Active inference and nonlinear dependence | none | — |
| Extreme fluctuations | survival curves, exceedance fractions, maxima, ES99+ and half-mass concentration across all receipted cells; finite-range tail fits (HT-13/15/17) | empirical, one scale, dependent population, own cap-off reference; no tail class |
| Generalised or coupled free energy | loss-level κ pilot (null); CAL-1 calibration checks | not the theory |
| Coupled Markov blankets | two software interfaces | unproven as blankets |
| Socioeconomic environments | none | — |

## F. One-paragraph version

We built the frozen prior, the small residual agent between two interfaces, prediction error as its learning signal
with two credit rules, and the audit machinery around it, and we measured editing, retention, locality and the
distribution of unintended harm on three datasets across three realizations and five orders. The experiment is a
driven, path-dependent system studied under continued driving, and its contact with the extremes is the harm
distribution: rare, concentrated, with tail shapes that differ by design, and controllable by an analytic one-nat bound
that needs no tail class. We ran a loss-level κ pilot, null under its pre-registered rule, and numerical calibration of
the coupled-entropy family. Expected-free-energy policy choice, the coupled free energy itself, precision as risk
sensitivity, epistemic audits and nested blankets remain proposed.
