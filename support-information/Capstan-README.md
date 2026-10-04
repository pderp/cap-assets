# Support information: what the caps actually say — worked examples (Capstan, 2026-10-04)

This folder shows concrete inputs and outputs behind the headline numbers, so that anyone can see what an "edit", a
"paraphrase", a "locality prompt" or a "near-miss" looks like and what each cap generated. Nothing here is a new
measurement: every answer is the greedy generation saved in the Stage-4 confirmatory cells (realization 0, order 100,
end-of-stream checkpoint 1,000 (300 for MQuAKE)), read from the sealed payloads and checkpoint files whose hashes are in `examples.json`.
The one thing computed for this document is the frozen base's own answer to each shown prompt (CPU, no cap).

## Files

- `examples-zsre.md`, `examples-counterfact.md`, `examples-mquake.md`: 30 edits per dataset (the first 30 in the
  stream order), then five locality prompts, five near-miss cases, three unseen prompts and the revision cases, each with
  every condition that ran at that coordinate.
- `examples.json`: the same content, machine-readable, with source hashes.
- **Second set, without the oldest-memories bias:** `README-random-sample.md` and `examples-<dataset>-random.md`, 30
  edits per dataset drawn at random (fixed seed) from the rest of the stream, with each item's stream position shown.
- Generator: `pc_cap/aw/support_examples.py` (`--mode first` and `--mode random`).

## How to read an item

Each edit is one fact to teach: a **prompt** (zsRE: a question; CounterFact: a sentence stem about a subject; MQuAKE: a
sentence stem whose answer is a single-hop fact used in multi-hop questions), a **new target** answer, and a held-out
**paraphrase** of the prompt. For CounterFact and MQuAKE the previously true answer is shown too; the edit is
counterfactual by design. The **base** line is what frozen GPT-2 small says with no cap at all: on zsRE questions it
almost always emits a newline at once (an empty answer), on CounterFact stems it continues with fluent but unrelated
prose, on MQuAKE stems it usually gives the old true fact or a guess.

The table under each item has one row per condition and three columns:

1. **right after the edit** — the answer generated immediately after the cap stored this fact (this is what the ES
   score counts; `[code]` marks an acquisition outcome other than `accepted`);
2. **end of stream, own prompt** — the same prompt asked again after all 1,000 (300 for MQuAKE) edits of the stream were stored
   (RET-ES: did the memory survive the later edits?);
3. **end of stream, paraphrase** — the paraphrase asked at the end of the stream (RET-GS: does the cap recognise the
   fact when asked differently?). This is the primary endpoint of the study and where the conditions differ most.

✓ means the registered scorer counted the answer as a success (full-answer alias match after normalisation), ✗ that it
did not. The scorer is strict: a correct answer followed by extra tokens, or a near-synonym not in the alias list, is ✗.

## The conditions

| label | what it is |
|---|---|
| learned reader v5 (primary) | the trained retrieval-and-null network with per-record delta writes; the system the talk is about |
| random-geometry reader + gate | the same gate and delta writes, but the reader's embedding is random (untrained): shows what the geometry alone buys |
| stable v0 cap | the first-month radius-gated cap with its stable write-free keys |
| matched-update adapter | the v0 cap's write rule applied through the v1 interface (a matched-compute comparator) |
| live v0 cap C1 / C2 | the original v0 cap with live keys, routing all three banks (C1) or one chosen bank (C2) |
| continued base (LM / literal) + stable cap | the base further trained on ordinary text (LM) or on the literal edit sentences, then the stable cap on top |

MQuAKE ran only the primary triplet (learned, random, stable v0) at 300 edits.

## Reading the three datasets

- **zsRE.** The base says nothing, so any answer is the cap's. The learned reader answers the paraphrase correctly in
  nearly every case; the random reader gets a third to a half; the v0 caps store the fact (own prompt ✓ right after the
  edit) but mostly cannot find it again from a paraphrase, and their own-prompt retention decays over the stream. Note
  that the 30 items shown are the *first* edits of the stream, i.e. the oldest memories by the end of it, which is
  why the v0 caps' end-of-stream retention here (about 1 in 30) is below their study-wide mean (0.66): their later
  edits overwrite or shadow the earliest ones; the learned reader keeps all of them.
- **CounterFact.** The stems invite free continuation, so the "answers" are short completions. Paraphrases carry a
  distracting prefix sentence; this is where the learned reader's null decision matters and where it still fails on
  roughly a third of items. The v0-family caps never fire on paraphrases here (their calibration matches exact prompts
  only), so their paraphrase column is the base's continuation.
- **MQuAKE.** Single-hop stems; the learned reader retains about 70 % of paraphrases at 300 edits (half of these 30);
  the random reader and stable cap retain none.
- **Unseen prompts.** For facts never stored, a changed answer means the cap fired on some other record (a false
  fire); the random reader does this most often, the v0 caps sometimes (occasionally landing on the right word by
  chance, since answers such as "midfielder" recur in the pool), the learned reader rarely. Whether a record fired is
  not stored in these rows, so only "answer changed" is shown.

## What these examples are not

Thirty hand-readable items per dataset, from one realization and one order; the study's numbers come from 1,000
edits × five orders × three realizations per condition (300 edits on MQuAKE) and are in `pc_cap/docs/R1_stage4_report.md`.
Base answers are shown for context only; they are not an endpoint of the study. Ordinary-text harm (the per-token
loss changes on 245,237 validation positions) is not shown here; see the HT-17 report for that.
