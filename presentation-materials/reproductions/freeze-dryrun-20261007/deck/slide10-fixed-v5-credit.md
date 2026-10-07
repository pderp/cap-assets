# Slide 10 — Does PC credit transfer to the fixed v5 reader?

**Draft speaker text for charlie's review. Completed exposed-stream comparison; reader-training replication is a separate study.**

**On screen:** behavior, harm and cost for the fixed-v5 paired comparison;
`diagram-specs.json`, slide `10`. Placeholders use the schema register
`pc-result-sources.json` and resolve only after completed real outputs exist.
Claim footer: `PC-fixed-v5`, `PC-mechanism`, `HT-readout`.

## Speaker text

“The second experiment asks whether the credit rule transfers to the learned
reader that retained edits in our main study. Both arms use the same original
BP-trained GPT-2, selected reader weights, calibration, gates, memory capacity
and stream order. Both begin with fresh memory. Only the delta-acquisition
credit changes: the registered adjoint path versus corrected eight-step error
inference. The reader itself remains trained by backpropagation.”
[`PC-fixed-v5`, `PC-mechanism`]

“This is deliberately small and exposed: realization zero of zsRE and
CounterFact, order one hundred, with three hundred edits each. It is a post hoc
transfer check, not fresh confirmation or three independent replications. We
use the installed R1 editing, retention, bounded-text locality, near-miss and
semantic revision functions. We evaluate at one hundred and three hundred
edits; ordinary-text harm is a separate readout on the full fixed inventory.”
[`PC-fixed-v5`]

“At the final checkpoint, SE-E minus SE-A is 0 for immediate editing
success and 0 for paraphrase retention on zsRE. The CounterFact
differences are 0 and -0.003333. Locality
differences are 0 and 0; near-miss differences are
0 and 0; semantic revision
differences are 0 and 0. Higher is
better for these behavior measures. If an assay is unavailable, that is shown
as unavailable rather than a successful zero difference.” [`PC-fixed-v5`]

“For unintended effects, the difference of the two arms' ES99 positive-harm
values is -0.01397 nats on zsRE and
0.01123 on CounterFact. Lower favors SE-E. Both
arms are evaluated on the same two hundred forty-five thousand, two hundred
thirty-seven ordinary-text positions. That gives matched predictions, not that
many independent experimental units.” [`PC-fixed-v5`, `HT-readout`]

“The stream-engine times sum to 604.6 seconds for SE-A and
776.7 for SE-E; the separate harm readout is
5004 seconds. Startup and lease wait are reported separately by
the driver. We need the behavior, harm and cost together before deciding whether
this credit rule is useful here. Whatever the outcome, autonomous policy choice
and coupled free energy remain proposed parts of the larger active-inference
programme.” [`PC-fixed-v5`, `AI-next`, `AI-programme`]

“A separate experiment trains the reader itself with predictive coding while
keeping acquisition adjoint. All twelve evaluations now pair three seeds.
ePC minus BP paraphrase retention is −2.67, −2.00 and +0.33 percentage points
on zsRE; CounterFact is −24.17, −2.17 and −17.50. Own-prompt retention is
nearly equal, with CounterFact seed one 1.00 for ePC versus 0.99 for BP.
The ePC readers fire less on ordinary zsRE text in every seed; CounterFact
firing and harm reverse direction across seeds. Training costs about one
hundred times BP. This is within-recipe evidence on one exposed subject
realization, not general superiority or safer learning.” [`PC-reader`]

## Backup: earlier checkpoint and exact sources

At the 100-edit checkpoint, paired differences (SE-E minus SE-A):

| Dataset | ES | RET-GS | LS | Near miss | Semantic revision |
| --- | --- | --- | --- | --- | --- |
| zsRE | 0 | 0 | 0 | 0 | 0 |
| CounterFact | 0 | -0.005 | 0 | 0 | 0 |

Behavior sources: PC-7 each cell's `checkpoint-100.json` / `checkpoint-300.json`
→ `metrics.<name>.value`, paired only after all four cells finish and their
inputs match. R1 semantic revision means latest-answer success AND old record
retired AND new record active. Harm uses the PC-5/6 `read_arm`/`pair` schema:
`difference_of_arm_es99.original`, `positionwise.original.loss.mean_signed`,
and per-arm `readout.summary.original`. The final 300-edit checkpoint is required
for this harm slot; a 100-edit readout does not fill it.

Sources: [driver record](../../tasks/PC-7.md), [adapter record](../../tasks/PC-6.md),
[claim ledger](../../talk_claim_ledger_v7.md). CPU parity and smoke results only
establish implementation readiness and cannot populate these result slots.
