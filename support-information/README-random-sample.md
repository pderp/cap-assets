# A second set of examples: 30 edits drawn at random from the rest of each stream (Capstan, 2026-10-04)

The first-30 files (`examples-<dataset>.md`) show the oldest memories of the stream, which biases the end-of-stream
columns against the caps that forget: by checkpoint 1,000 those items have had 970 later edits stored on top of them.
This set removes that bias. For each dataset, 30 stream positions were drawn uniformly at random, without replacement,
from positions 30+1 to the end of the stream (1,000 for zsRE and CounterFact, 300 for MQuAKE), with a fixed seed
(20261004) so the draw is reproducible and was made once, before looking at any outcome. Everything else is identical to
the first set: same cells (realization 0, order 100), same checkpoint, same conditions, same scorer, same base-answer
decode. Files: `examples-zsre-random.md`, `examples-counterfact-random.md`, `examples-mquake-random.md`,
`examples-random.json`. Each item's heading gives its stream position, so you can see how many later edits each memory
had to survive.

What the position mix changes (compare each file's counts table with the first-30 file): on zsRE the v0-family caps'
end-of-stream own-prompt retention rises from about 1/30 to 9–13/30 (study-wide mean 0.66 over all 1,000 edits; later
positions have had fewer edits stored on top of them), and their paraphrase retention from 1/30 to 2–4/30; the random
reader's paraphrase retention is 17/30 (first set 11/30; study-wide 0.52); the learned reader keeps all 30 own prompts
and all 30 paraphrases in both sets. On CounterFact the two sets give the same picture (learned 21/30 paraphrases,
random 5/30, v0 family 0/30, own-prompt retention complete for every cap). On MQuAKE the learned reader's paraphrase
retention is 24/30 in this set against 15/30 among the first 30 (study-wide 0.70); the random reader and stable cap
retain none in either. These remain hand-readable samples, not the study's estimates.
