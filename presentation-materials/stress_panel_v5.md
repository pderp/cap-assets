# Stress panel — old-fact recovery under continued editing (development, 2026-09-17)

Source: pc_cap `results/R1/stage4_dev_cells/ht_panel/` (six cells, commit b4a063d), design `manifests/revision_v1/ht_development_panel_v1.json`, DEC-055.

Six development cells on primary v5 through Codex's HT-5 supervisor (`docs/tasks/HT-5-panel-v5/`, budget account
`results/R1/stage4_dev_cells/ht_panel/_budget/`): 1,310 s charged of the 14,400 s ceiling, ≈ 215 s per cell, no
failures. 100 attempted edits per cell (20 warm-up, 40 treatment, 40 later), old-fact probes = the first 20 facts,
teacher-forced target-token NLL and exact answers at edits 20 / 60 / 70 / 80 / 100, reference = the cell's own
edit-20 state.

| dataset | schedule | exact old answers at 100 | mean positive ΔNLL vs edit 20 (nats / token) at 60 / 70 / 80 / 100 | worst fact (mean over its tokens) | max token Δ | recovery |
| --- | --- | ---: | --- | --- | ---: | --- |
| zsRE | shuffled = clustered | 20 / 20 | 0 / 0 / 0 / 0 | none | 0 | [0, 0] (never harmed) |
| CounterFact | shuffled = clustered | 20 / 20 | 0 / 0 / 0.324 / 0.324 | cf-20223 +4.0, cf-45 +2.5 | 12.5 | none, right-censored > 40 updates |
| MQuAKE | shuffled = clustered | 20 / 20 | 0.112 / 0.112 / 0.112 / 0.112 | mquake:9405b94b… +2.0 | 6.6 | none, right-censored |

Three observations. (1) **Schedule does not matter for this reader**: the shuffled and clustered arms give identical
numbers to four decimals on every dataset. The memory is a set of records with hard top-1 selection and per-record
deltas; the state after the same 60 or 100 facts is the same whatever the order, so the "clustered difficult items"
stress finds nothing to stress. That is itself the result of HT-2's cadence hypothesis: no order effect on this
substrate. (2) **Harm is item-determined, sparse and permanent**: on CounterFact two of the twenty probed facts lose
2.5 and 4.0 nats per token on average (one token loses 12.5 nats) after one of edits 71–80 enters memory, and on
MQuAKE one fact loses 2.0 nats (max 6.6) after the treatment block; nothing changes afterwards because nothing
in the reader revisits a stored record — recovery is not a process this design has, so the lag is right-censored at
40 updates in every harmed cell. (3) **Greedy answers hide it**: exact old answers stay 20 / 20 everywhere; the harm is
in the probability mass, which is exactly the tail argument of the talk (HT-1b) at the scale of single facts. zsRE's
short answers are untouched.

The CounterFact and MQuAKE harm coincides with a later edit whose subject or answer shares tokens with the probed
fact (the reader's rare-token gate admits a selection on the probe prompt once such a record exists); the per-token
rows (`ht_relative.token_rows`, `delta_from_edit20`) and the edit history in each checkpoint identify the pair.
Development only; three datasets, one seed each; the panel's role in the talk is the recovery-lag slide, whose
honest content is "no recovery mechanism, harm is permanent and localized".

## How to say it

- "Does the cap recover from interference?" — Not within the study window: sparse probability degradation of old facts appeared after a later edit and persisted through edit 100; recovery was unobserved (CounterFact: harmed at 80, 20 later updates observed; MQuAKE: harmed at 60, 40 later updates). Why it persists is a hypothesis (no mechanism in the design revisits a stored record), not a measured cause.
- "Does the editing schedule matter?" — The two tested schedules (shuffled vs clustered difficult items) produced identical observed trajectories on every dataset — for these schedules and this seed; not a proof of universal order invariance.
- The harm is invisible to primary exact-match scoring (20 / 20 old answers everywhere; paraphrase retention 0.8 / 0.6 on CounterFact / MQuAKE) and large in probability (up to 12.5 nats on one token): the same mean-versus-tail point as the drift audit, now on named facts.
- Development cells, one seed, 100 edits, three datasets; not confirmatory.
