# Slide 9 — Corrected PC-v0: efficacy, harm and cost

**Draft speaker text for charlie's review. Result slots remain pending until
completed research reports exist; this file contains no invented PC outcome.**

**On screen:** paired SE-E minus SE-A paraphrase retention, positive-harm ES99
and cost. Use `diagram-specs.json`, slide `09`. Every numerical result below is a
slot resolved by `aw/presentation_pc.py` from `pc-result-sources.json`. The paths
in that register are configured future outputs, not assertions that they exist.
Claim footer: `PC-v0`, `PC-SD24`, `HT-readout`.

## Speaker text

“This comparison brings predictive coding directly into the experiment. We keep
the cap, frozen base, teaching stream and update constraints fixed and change
the acquisition credit. SE-A uses the adjoint; SE-E infers errors for eight steps
with the corrected energy. In particular, the prior penalty now applies to the
inferred error before adding the cap's write. The old defective-energy results
are a historical reference, not a control pooled into this comparison.”
[`PC-mechanism`, `PC-SD24`, `PC-v0`]

“The population is the exposed historical S5 stream: zsRE ends at one thousand
edits and CounterFact at three hundred. There are three realizations and five
dependent orders per realization. This is a supplemental defect-correction
replication. The primary scores retain the old S5 conventions; bounded-text
secondary scores are kept separate, rather than silently changing the measure.”
[`PC-v0`]

“On zsRE, SE-E minus SE-A is PENDING for immediate editing success and
PENDING for final paraphrase retention. The three realization retention
differences are PENDING. On CounterFact, the corresponding
means are PENDING and PENDING, with retention
differences PENDING. Locality differences are
PENDING and PENDING, respectively. Higher behavior scores
favor SE-E. A null or adverse difference is part of the answer.” [`PC-v0`]

“We must put harm beside efficacy. On the same preselected ordinary-text
positions, the mean difference of the two arms' ES99 positive-harm values is
PENDING nats on zsRE and
PENDING on CounterFact. Lower favors SE-E here.
These are differences of arm tail summaries, not the ES99 of positionwise
differences. The readout retains all unchanged positions and compares against
the same frozen base. It describes concentrated loss; it does not establish
an asymptotic heavy-tail family.” [`PC-v0`, `HT-readout`]

“SE-A's summed process time is PENDING seconds; SE-E's is
PENDING. The separately charged harm readout takes
PENDING seconds. Process time includes startup, acquisition and
evaluation; it is not a pure credit-kernel timing. We report this cost alongside
the measured effect. This tests one predictive-coding mechanism, not a complete
active-inference agent or a general claim that PC is superior.” [`PC-v0`, `AI-testbed`]

## Source and interpretation notes

- PC-3 table `aggregates`: select `dataset` and `metric` (ES, RET-ES, RET-GS,
  LS); read `mean`, `realizations`, `minimum`, `maximum`. Cost comes from `cells`
  → `finish.elapsed_process_seconds`; operation counters remain in its ledger.
- PC-5 `pairs[*].difference_of_arm_es99.original`, averaged over the same paired
  cells by dataset. `positionwise.original.loss.mean_signed` gives the paired
  mean loss difference. The position inventory is the legacy S5 32-window,
  4,064-target set, not the R1 full-validation set.
- Require the complete 60-cell design and matching source identities. Missing
  reports render **PENDING**, unavailable metrics **UNAVAILABLE**, and CPU-smoke
  artifacts are refused. No token-level interval or five-orders-as-five-seeds
  interpretation is allowed. Full realization/order tables remain backup.

Read [PC-v0 specification](../../additional_work/PC-v0.md) and
[claim ledger](../../talk_claim_ledger_v7.md). Lead review still chooses the final
spoken interpretation after seeing the completed effects, harm and costs.
