# Capstan review, round 5 (2026-10-08, export of 10:58, 30 slides)

Read in full as images. The duplicate title slide is gone, the closing slide now matches slide 1, the mean-KL benchmark has its units, and the mixture slides both say "ten realization-0 streams". All 14 links are unchanged and valid. Every number still matches the record.

Because slide numbers keep shifting, this list is keyed by **slide title or first words**, not by number. Each item says exactly what to change and is marked done when it appears in an export.

## A. Typos introduced by the last round (fix)

| Slide (by title) | Problem | Change to |
|---|---|---|
| "The probability mixture (bounded correction)" | last paragraph: "Measured on the the ten realization-0 streams" | "Measured on the ten realization-0 streams" |
| "The mixture reduced severity to about one-third." | caption now says both "(five orders × two datasets)" and ": two datasets × five orders at 300 edits" | "Mean loss increase among positions with Δ > 0.01 nat, on the ten realization-0 streams (two datasets × five orders) at 300 edits." |

## B. Optional content additions still open (from Capstan.md §3; your call)

| Slide (by title) | Addition | Text to paste |
|---|---|---|
| "Retrieval is central" | the two numbers behind the claim | "Over four independent realizations the learned reader beat the random reader by 44 points of paraphrase retention on zsRE and 56 on CounterFact. Writing only at the last site kept paraphrase retention within 0.7 points but raised ordinary-text harm 2.6–4.4× in all twelve paired comparisons." |
| "Training the reader with predictive coding gave mixed outcomes." | why "mixed": the cost | append to the caption: "ePC training took 96–102× the backprop time (23–25 hours versus about 15 minutes per seed)." |
| "Extreme losses have different observed tails" (figure) | legend wording | "Saved exponential fit" → "Exponential fit to excesses above 0.01 nat" (needs re-export of the figure; skip if inconvenient) |

## C. Cosmetic (your call)

| Slide (by title) | Item |
|---|---|
| title slide and "Questions?" slide | the ASCII arrow "—--------------->>>>>" |
| "The following are final scores averaged over orders ..." | no title; suggested "Paraphrase retention after 1,000 edits (300 for MQuAKE)" |
| "Frozen GPT-2 and the selected v5 reader; only acquisition credit changes." | no title; suggested "Changing only the acquisition credit (one realization, 300 edits)" |

## D. Verified in this export (no action)

- "Lessons learned" says "the next 4 slides"; the four that follow are Retrieval is central, Predictive Coding still has tradeoffs, A simple bound was useful, The wider theory is still open. Correct.
- All six definition slides match Capstan3.md; the settling table matches Capstan2.md; slides 3 ("This presentation was submitted as"), "Predictive Coding", "Error Predictive Coding", "Predictive Coding still has tradeoffs" and "Affiliations" carry the round 1–2 corrections.
- Order: title · Predictive Coding Cap Experiments · submitted as · objectives · datasets and repositories · Predictive Coding · Error Predictive Coding · What a cap is · Two generations · How an edit is taught · The procedure · What we measure · final scores table · tradeoff text · fixed-v5 credit table · PC-trained reader table · tail figure · mixture definition · mixture result · settling table · Scale and compute · Lessons learned · four lessons · Further work · Coupled Entropy · Affiliations · Questions. This is the order recommended in Capstan3.md §3.

Once section A is done, nothing I have raised remains open except the optional items in B and C.
