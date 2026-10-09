# Systems far from equilibrium, and where this project does and does not touch them

Prepared for charlie by Capstan, 2026-10-09. The talk is in a satellite called *Thriving in the Extremes: Active
Inference in Non-equilibrium Systems*, and the submitted abstract promised a "risk-aware residual agent for
non-equilibrium regimes". This note explains what "far from equilibrium" means from first principles, how the
satellite's community uses the phrase, and then goes through our experiments and says, for each, whether the
connection is real, metaphorical, or only proposed. The companion file `abstract-vs-what-was-built.md` is the
claim-by-claim ledger. Sources are the record (`docs/presentation/abstract_to_testbed.md`, `qa.md`,
`docs/additional_work/HT-17_report.md`, `coupled_objective_note.md`, `assets/presentation-materials/kappa_pilot_v5.md`)
and the abstract itself.

## 1. Equilibrium, near equilibrium, far from equilibrium

**Equilibrium** is the state a closed system settles into when nothing drives it. In physics it has sharp properties:
no net flows of anything (energy, matter, probability) between parts of the system; every microscopic process is
balanced by its reverse ("detailed balance"); the state is the one of maximum entropy compatible with the constraints;
it has no memory of how it was reached; and its fluctuations are small and Gaussian, with a variance set by a
temperature. A cup of tea that has cooled to room temperature is at equilibrium. So, in a looser sense, is a neural
network trained to convergence on a fixed dataset: the weights have stopped moving, the gradient averages to zero, and
the order in which the data were shown no longer matters.

**Near equilibrium** means the system has been nudged slightly and is relaxing back. The response is linear in the
nudge, relaxation is exponential in time, and the small-fluctuation picture still holds. Most of classical statistical
physics, and most of the intuition behind gradient descent "settling into a minimum", lives here.

**Far from equilibrium** means the system is being driven continuously and strongly enough that it never gets to
relax. Energy or matter or information flows through it all the time. Several things then change qualitatively:

- There are sustained **fluxes** and ongoing **entropy production**; the system is open, and its order is maintained
  by throughput, not by stillness. A living cell, a hurricane, a market, a brain.
- The state is **history-dependent**: the path matters, not just the present forcing.
- Fluctuations stop being small and Gaussian. They become **heavy-tailed**: rare events are far more common and far
  larger than a bell curve would predict, so that averages can be dominated by a handful of extremes, and in the
  limit the variance can be infinite.
- Structure can appear and persist only because of the driving ("dissipative structures"); remove the throughput and
  the structure dies.

The satellite takes the biological reading of this. Living and cognitive systems are far-from-equilibrium systems
that persist by keeping themselves in a narrow band of states despite a turbulent environment. Active inference, in
Karl Friston's formulation, is the claim that such a system can be described as minimising a variational free energy
(a bound on the surprise of its sensations), with a **Markov blanket** separating its internal states from the
environment so that the two are conditionally independent given the blanket. Kenric Nelson's **coupled entropy**
programme adds the heavy-tail half: ordinary (Boltzmann or Shannon) entropy and the ordinary free energy assume
exponential tails, and a single coupling parameter κ generalises the logarithm and exponential to families with
power-law tails (the generalised Pareto, or "coupled exponential", is the κ > 0 member). The satellite's two framing
questions were therefore: how do cognitive agents survive and learn in extreme, non-equilibrium environments, and how
should the mathematics of active inference be generalised for heavy-tailed systems.

## 2. The abstract's picture, in that vocabulary

The July abstract maps this onto a language model. A pretrained transformer is a generative prior that is accurate on
the bulk of its training distribution and fragile in the extremes (rare domains, distribution shift, non-stationary
deployment streams), where its residual errors "turn heavy-tailed". A small adaptive agent sits between the frozen
transformer and the environment, learns only the residual R = F* − F₀ as a prediction error, and talks to each side
through a Markov blanket whose porosity is set by the same κ that sets the error tail-weight. The agent is
"risk-aware" because it refuses to act under low evidence, and it "thrives in the extremes" because the coupled free
energy keeps its precision finite on tail events.

That is the hypothesis. What follows is what was built and measured against it.

## 3. Where the connection is real

### 3.1 The experiment is a driven, open, path-dependent system

A continual-learning stream is the closest thing in machine learning to a driven system. The cap is never trained to
convergence on the whole stream. Each edit is a perturbation applied once; the next edit arrives before the previous
one has been "digested" in any global sense; nothing is ever re-balanced. Three features of the design are exactly the
features that distinguish driven from equilibrated systems:

- **History dependence is a measured variable.** Every cell is run in five different orders of the same facts, and
  the record keeps the per-order values. Order effects are interference: the trace of earlier perturbations being
  overwritten or displaced by later ones. An equilibrated learner would show none.
- **The checkpoints are measurements of a system under continued driving.** Retention at 100, 300 and 1,000 edits is
  the fraction of earlier perturbations that survived the driving since. (See `checkpoint-explanation.md`.)
- **The base never equilibrates with the cap** because it is frozen. The cap is the only thing that moves, and it is
  driven from outside by the edit stream. This is the "frozen prior plus small residual agent" of the abstract, built
  as described, at GPT-2-small scale.

This is a real structural correspondence, not a metaphor, with one caution: nothing thermodynamic is being measured.
There is no energy flux, no entropy production rate, no temperature. The correspondence is at the level of "open,
driven, path-dependent, never relaxed", which is the dynamical-systems reading of non-equilibrium, not the physical one.

### 3.2 The harm distribution is the project's actual contact with "the extremes"

The strongest empirical link to the satellite's theme is the ordinary-text harm measurement. Every cell scores the same
245,237 positions of ordinary text with the cap on and off. The result has the signature that non-equilibrium
statistics predicts and Gaussian statistics does not:

- Harm is **rare and concentrated**. For the learned reader, only 0.16 % of positions (zsRE) and 0.30 % (CounterFact)
  change by more than 0.01 nat, yet half of all harm sits in 0.03 to 0.06 % of positions, and single positions reach
  11 to 15 nats. The mean harm is tiny; the tail is where the damage lives.
- **Averages mislead.** This is why the deck reports the mean next to ES99+ (the mean of the worst 1 %), the fraction
  above three thresholds, and the maximum, rather than one summary. That reporting choice is a direct import from
  heavy-tail practice (ES99+ is an expected shortfall, the risk measure used precisely because variance is not
  trustworthy when tails are heavy).
- **Different caps have different tail shapes.** The HT-17 analysis fitted generalised-Pareto excesses, the κ > 0
  family of Nelson's framework, to each cell. Stable v0 on zsRE has a clearly heavier-than-exponential fitted tail
  (shape 0.43 to 1.03 across cells, better held-out likelihood than an exponential in all fifteen). The learned reader's
  fitted shapes have intervals that include zero: an exponential tail describes it about as well. So the two cap
  designs differ not only in average harm but in how extreme their worst events are relative to their typical ones.

What this does **not** establish, and the Q&A document is firm on it: no asymptotic tail class, no power law, no
infinite variance, no entropy growth with system size. The population is one model at one scale, the same text
repeated across cells, and the orders are dependent. These are finite-range fitted shapes on dependent data. The
honest sentence is "the harm is heavy-tailed in the practical sense that the worst 0.05 % of positions matter more than
the mean, and the two cap designs differ in fitted tail shape"; the dishonest sentence would be "we found a power law".

### 3.3 The one-nat bound is a non-equilibrium-style guarantee that does not need the tail class

The probability mixture (ρ = e⁻¹ of base, the rest cap) is the clearest "thriving in the extremes" result, and the
reason is instructive. It guarantees, by a one-line inequality, that no single token's loss can rise by more than one
nat, whatever the cap does. It therefore cuts the conditional severity of harmful events by about three times
(1.619 → 0.542 nats on zsRE, 1.925 → 0.581 on CounterFact) and brings the worst observed losses from 9 to 15 nats down
to 1.00, while leaving editing endpoints essentially unchanged.

The connection to the satellite's question is this: when you do not know the tail class, and cannot know it from a
finite sample, a bound that holds regardless of the tail is worth more than a fitted shape. This is the practical
answer to "how does an agent persist in a regime whose extremes it cannot characterise": it caps its own exposure
analytically rather than estimating the exposure statistically. HT-17 makes the point sharply: the generalised-Pareto
fits to the mixture's harm all fail (invalid endpoints), which is what you expect when a hard ceiling has been imposed,
and the ceiling holds anyway.

### 3.4 Refusal under low evidence was built and measured

The learned reader's null option (null mass ≥ 0.5 means no write, output equals the base exactly) is the "refuse to
act under low evidence" of the abstract. It is a hard rule, not an expected-free-energy policy, but it is real, it is
what separates the learned reader from the radius-gated v0 (which "often reads the wrong record"), and its failure
mode is measured directly as false fires on unseen prompts and near-miss prompts.

## 4. Where the connection is only metaphorical, or runs the other way

### 4.1 Predictive-coding "settling" is an equilibrium computation

This is the one place where the project's vocabulary and the satellite's vocabulary point in opposite directions, and
it is worth being clear about it. The error-inference credit starts error states at zero and relaxes them for k steps
to minimise a quadratic energy plus the answer loss. That is descent to the minimum of an energy function with
everything else held fixed: a near-equilibrium relaxation in the most literal sense. The deck's "settling" is
settling *toward* equilibrium. The "equilibrium propagation" family of algorithms to which this belongs takes its
name from exactly that.

So "we used predictive coding" is not in itself a non-equilibrium claim. Predictive coding enters as a credit
assignment rule inside one edit, and that rule is an equilibrium computation. The non-equilibrium character of the
experiment comes from the stream around it (section 3.1), not from the settling inside it.

### 4.2 No free energy was minimised, coupled or otherwise

The abstract's agent minimises a coupled free energy. The built agent minimises an ordinary cross-entropy on the taught
answer (for writes) and an ordinary classification loss (for the reader's training). The κ pilot replaced the reader's
answer surprisal −ln p by a bounded deformation (1 − e^{−κℓ})/κ for κ ∈ {0.2, 0.5}. That is a loss-level change, not
Nelson's coupled free energy: there is no coupled expectation, no escort distribution, no change to the inference
distribution. Under its pre-registered rule the pilot was null: both κ arms reduced the tail and the false-fire rate but
cost more paraphrase retention than the declared floor allowed, and a plain clipped surprisal achieved most of the same
tail reduction. Descriptively it showed that bounding surprisal shifts the porosity/interference trade-off rather than
improving it. The record is explicit that this neither confirms nor refutes the coupled-entropy programme; it tested a
different object.

### 4.3 The "Markov blankets" are software interfaces

Two interfaces exist: the query interface with the null decision (environment side) and the read taps plus bounded
writes at the three sites (prior side). The abstract calls them Markov blankets and says their porosity is κ-tuned.
Nothing was measured about conditional independence across either interface, and the write budget and null threshold,
which are the two "porosity knobs" the system actually has, are fixed numbers unrelated to any tail parameter. The deck's
"Further work" slide says this plainly. The label is a label.

### 4.4 Nothing acts on the environment, and nothing seeks information

Active inference needs a policy chosen by expected free energy, with a preference model and an epistemic term. The
built system has a fixed routing rule (fire or do not fire) and the investigators choose every probe. The "learn from
failure" theme of the satellite is true of the people who ran the programme (the ordinary-text drift assay, the
unseen-prompt false fires and the MQuAKE null instability were each found by looking where the system failed, and each
changed the design) but not of any agent in the loop.

## 5. The honest summary

If asked "what does this have to do with systems far from equilibrium?", the defensible answer has three layers:

1. **Structurally**, the experiment is a driven open system studied under continued driving: a frozen prior, a small
   adaptive layer perturbed once per fact in five orders, measured at fixed checkpoints for what survived. Interference
   and forgetting are path dependence, measured. That is the dynamical-systems sense of non-equilibrium, and it is
   real.
2. **Empirically**, the project's contact with "the extremes" is the harm distribution: rare, concentrated, with the
   worst 0.05 % of positions carrying half the damage, with fitted tail shapes that differ between cap designs, and
   with a bound (the one-nat mixture) that controls the extremes without needing to know their class. That is the
   satellite's "extreme fluctuations" objective, met descriptively at one scale.
3. **Theoretically**, the coupled free energy, κ-porous blankets, expected-free-energy policy and precision-as-risk
   were proposed and not built. The one pilot in that direction tested a loss deformation, not the theory, and was
   null under its rule. The CAL-1 note sets out what a real implementation would have to decide first (which random
   variable, which functional, how to differentiate the escort normalisation), and that is post-conference work.

And one sentence to keep in mind when the word "equilibrium" comes up in questions: the predictive-coding settling
inside each edit is an equilibrium computation; the non-equilibrium content of the talk is the stream, the tails and
the bound, not the settling.

## 6. Terms the audience will use, in one line each

| Term | Meaning at this satellite | Our nearest object |
| --- | --- | --- |
| Non-equilibrium steady state | a system held in a narrow band of states by continuous throughput | the cap under a stream; not steady, since it never stops accumulating records |
| Dissipative structure | order maintained only by driving | none |
| Heavy tail / power law | rare events far larger than Gaussian predicts; variance may not exist | ordinary-text harm: concentrated, finite-range fitted shapes; no class claimed |
| Generalised Pareto / coupled exponential | the κ > 0 family of tails in Nelson's framework | HT-17 fits of harm excesses |
| Expected shortfall (ES) | mean of the worst fraction of outcomes | ES99+ on every harm readout |
| Variational free energy | bound on surprise minimised by a self-organising system | not implemented; ordinary cross-entropy losses instead |
| Coupled free energy, calibrated entropy | κ-generalised free energy and entropy with power-law reference | proposed; CAL-1 numerical checks only |
| Markov blanket | states that render inside and outside conditionally independent | two software interfaces, unproven as blankets |
| Expected free energy, epistemic value | policy selection that trades preferred outcomes against information gain | fixed gate; investigator-chosen audits |
| Precision | inverse variance weighting of prediction errors | per-site scaling inside the ePC solver; not used as risk |
| Equilibrium propagation / settling | relaxation of internal states to an energy minimum before a local update | the error-inference credit (an equilibrium computation) |
