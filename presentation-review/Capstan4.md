# Capstan review, round 4 (2026-10-08, export of 10:49, 31 slides)

Read in full as images, not diffed. All six definition slides are in and placed as suggested (A–C after "Error Predictive Coding", D after "The procedure", F before the mixture result, E after the settling table). Every number on the deck still matches the record. All fourteen hyperlinks resolve to the right targets, including the two new repository links.

## Fix before the talk

1. **Slides 1 and 2 are the same slide.** The title slide appears twice. Delete one.
2. **Slide 31 (closing) still has the old title**, "Thriving in the Extremes Presentation", while slide 1 now reads "CSS2026 satellite: Thriving in the Extremes". Make them match.

## Small inconsistencies worth one edit each

3. **Slide 19 says "ten sealed streams"; slide 20 says "ten exposed memories".** Same ten runs (realization 0, five orders × two datasets, 300 edits). Both words are used in the record for different aspects (the subjects were exposed in development, the order files were sealed), but side by side they look like two different experiments. Use one phrase on both, for example "the ten realization-0 streams (five orders × two datasets)".
4. **Slide 15, "benchmark of 0.001"** still has no units or object. Suggest "mean KL ≤ 0.001 nats per token on ordinary text" (Capstan.md §3.6).

## Recommendations from Capstan.md §3 not yet taken (optional)

5. **Slide 24, "Retrieval is central"**, still carries no number. Two one-liners would make it concrete: the Option R replication (learned reader beats the random reader by 44.1 points of paraphrase retention on zsRE and 56.2 on CounterFact over four realizations) and the upper-layer result (writing only at the last site kept paraphrase retention within 0.7 points but raised ordinary-text harm 2.64–4.37× in all twelve paired comparisons). The random reader is now defined on slide 10, so the first number has its setup.
6. **Slide 17 caption** does not say why the PC-trained reader's outcome is "mixed": measured ePC training time was 96–102× backprop (23–25 hours versus about 15 minutes per seed). One clause in the caption.
7. **Slide 18 legend**, "Saved exponential fit", does not say what was fitted; "exponential fit to excesses above 0.01 nat" is the accurate label. Optional.

## Cosmetic, your call

- The ASCII arrow on slides 1, 2 and 31.
- Slides 14 and 16 have no title ("Paraphrase retention after 1,000 edits (300 for MQuAKE)"; "Changing only the acquisition credit (one realization, 300 edits)").
- With 30 content slides, slide 22's "The next 4 slides" is still correct (23–26).

## Verified unchanged

Slides 9–11, 13, 19, 21 match the text supplied in Capstan3.md. Slide 15 table matches Capstan2.md. Slides 14, 16, 17, 18, 20 match the record as checked in Capstan.md §2.
