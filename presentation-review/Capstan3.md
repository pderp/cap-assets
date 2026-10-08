# Capstan review, round 3 (2026-10-08, export of 10:16)

## 1. Check of the new export

Text diff against the 09:58 export: slide 1 title ("CSS2026 satellite: Thriving in the Extremes"), slide 3 heading ("This presentation was submitted as: ..."), slide 6 full stop, and slide 18 (rewritten as recommended) are the only changes. Links unchanged and all valid. Nothing from `Capstan.md` §1 or §2 remains open. (Correction, 10:25: I first wrote here that the slide 15 table was still the old one. It is not: the export carries the new seven-column table and every cell matches `Capstan2.md` §2. The table is an image in the PDF, so my text diff did not see it.)

Still open from the cosmetic list, your call: the ASCII arrow on slides 1 and 24, and the untitled tables on slides 9 and 11.

## 2. Definition slides to squeeze in

Six slides, each written to fit one Google Slides body at the deck's current type size (about 60–80 words on the slide; the speaker note is for you, not the slide). Every number is from the reviewer primer (`pc_cap/docs/friday-10.02-review/README.md` §3–4) or the consolidated report. Suggested placement is given for each; the order below is the order they would appear in the deck.

---

### Slide A: "What a cap is"
**Place after slide 7 (Error Predictive Coding), before "The procedure".**

> **The base** is GPT-2 small: 12 blocks, 124M parameters, frozen throughout. No base weight ever receives a gradient.
>
> **The cap** is a small adaptive module attached to the base at three **sites**: the residual stream after blocks 4, 8 and 12. At each site it can **read** the current activations and **write** a correction vector into them. Writes share one size budget; a zero write reproduces the base exactly.
>
> **The memory** holds one **record** per taught fact: a key (an embedding of the prompt) and a payload (the write vectors that produce the new answer). Records are append-only; the reader decides at query time which record, if any, applies.

Speaker note: the first-month "v0" line used a different base, a 50M-parameter GPT-2-shaped model distilled from GPT-2 by error predictive coding (50M tokens, 12 GPU-hours, mean KL to the teacher 3e-5 nats per token), so that PC credit could be tested on a PC-trained base. That is what "legacy 50M ePC base" means on slide 15.

---

### Slide B: "Two generations of cap: stable v0 and the learned reader"
**Place right after slide A.**

> **Stable v0** (first month). Three radius-gated memory banks, one per site. A query fires a bank when its embedding is within a calibrated radius of a stored key; the stored write is added. Writes are taught by gradient steps on a fixed schedule. It stores usable corrections (an oracle read gives 94% paraphrase success) but often reads the wrong record, because a radius cannot tell a paraphrase of a stored fact from a prompt about a neighbouring fact.
>
> **Learned reader** (v1; the selected checkpoint is called **v5**). A 3.35M-parameter network trained by backprop to decide, once per query, whether any stored record applies. It embeds the prompt, scores it against the nearest stored keys, and keeps a **null** option: null mass ≥ 0.5 means no write at all, so the output equals the base to the bit. Otherwise the best record's write vectors are applied.
>
> **Random reader** (control). Same gate and write mechanism, but the reader's geometry is random rather than trained.

Speaker note: "v5" is the unweighted average of checkpoints 150–300 of one training run, selected on development data and frozen before the confirmatory study began; every "learned reader" number in the deck is that one artifact. The random reader is what the +44 / +56 point replication (Option R) is measured against, if you add that number to slide 17.

---

### Slide C: "How an edit is taught and credited"
**Place after slide B, or merge into slide 8 ("The procedure").** This defines "adjoint", "error inference" and "settling steps" before slides 11, 15 and 18 use them.

> **Teaching one fact.** The cap's write vectors for that fact are moved a few small steps in a direction that lowers the loss on the target answer, with the base frozen. The direction is the **credit**.
>
> **Adjoint credit.** Differentiate the answer loss back through the frozen base (ordinary backprop) and take the negative, normalised gradient.
>
> **Error-inference credit** (predictive coding). Start a temporary error state at each site at zero. Relax the error states for *k* **settling steps** against a quadratic error penalty plus the answer loss, holding everything else fixed. Use the settled error at each site as the direction.
>
> **One settling step from zero gives exactly the adjoint direction.** Whatever eight or thirty-two steps add is the content of the settling.

Speaker note: in the delta rule actually used, each fact gets at most five normalised steps at learning rate 0.1, stopping when the support loss falls below 0.1 and rolling back if the final loss is not below the initial loss. Both credit rules use that same bounded update; only the direction differs.

---

### Slide D: "What we measure"
**Place before slide 9 (the first results table).**

> Each run teaches 1,000 facts one at a time (300 for MQuAKE) and scores by plain greedy generation at checkpoints 100, 300 and 1,000.
>
> **Edit success**: the new answer appears right after teaching.
> **Own-prompt retention**: at the end of the run, the original prompt still gives the taught answer.
> **Paraphrase retention** (the primary endpoint): a held-out rewording of the prompt gives the taught answer.
> **Locality / near-miss**: unrelated prompts, and prompts about a neighbouring fact, still give the base's answer.
>
> **Harm**: the cap's effect on 245,237 positions of ordinary text (OpenWebText), measured per token as Δ = loss with cap − loss without cap, in nats. We report the mean, the fraction of positions with Δ above 0.01, 0.1 and 1 nat, the maximum, and **ES99+**, the mean Δ over the worst 1% of positions.
>
> **Realization / order**: an independent draw of facts from the dataset / a permutation of that draw. Three realizations × five orders in the main study.

Speaker note: the old project benchmark for harm is mean KL between cap-on and cap-off next-token distributions ≤ 0.001 nats per token; it is the line that all 45 learned-reader cells exceed (slide 10). Positions are not independent draws: the same 245,237 positions recur in every cell, which is why we compare cells to each other rather than quote confidence intervals on a single cell.

---

### Slide E: "Scale and compute"
**One line to add to slide 8 or to slide A; or its own slide before "Lessons learned".**

> Everything in this talk is GPT-2 small (124M parameters) on one local GPU. The confirmatory study ran 270 cells in 392 process-hours; the supplemental studies after it (Option R, settling controls, the PC-trained reader, the upper-layer interface, bounded correction) added about 153 process-hours. Transfer to production-scale models is not established.

Speaker note: "process-hours" is the sum of per-process time on a single GPU and double-counts concurrent processes; GPU occupancy for the supplemental work was 136 hours over a 170-hour span.

---

### Slide F: "The probability mixture (bounded correction)"
**Place immediately before slide 14 ("The mixture reduced severity to about one-third"), or make it the top half of slide 14.**

> At query time, mix the cap's next-token distribution with the frozen base's:
>
> p = ρ · p_base + (1 − ρ) · p_cap,  ρ = e⁻¹ ≈ 0.37
>
> The cap keeps 63% of the probability mass, so the greedy answer is unchanged wherever the cap was already winning. The base's 37% share guarantees that **no single token's loss can rise by more than −ln ρ = 1 nat** at the same prefix.
>
> Measured on the ten sealed streams: editing endpoints unchanged on zsRE, paraphrase retention −0.7 to −1.2 points on CounterFact, worst token loss 9–15 nats → 1.00, mean harm and worst-1% harm cut 3.2–3.5×.

Speaker note: this was pre-registered as an intervention experiment, "what bounding does to the tail and what it does not do", not as a recommended configuration. It bounds per-token loss at a fixed prefix; it does not promise unchanged greedy answers in general, and CounterFact's mean KL stays above the 0.001 line. Twelve other wrappers were tried first; every clip of the log-ratio destroyed editing because it bounds how far the answer token may rise.

---

## 3. Resulting order (24 → 30 slides)

1–7 as now · **A** what a cap is · **B** two generations · **C** teaching and credit · 8 procedure (+ **E** compute line) · **D** what we measure · 9–13 as now · **F** mixture · 14 · 15 (new table) · 16–24 as now.

If the slot forces cuts, keep A, B and D; fold C into slide 7's last paragraph (one sentence: "one settling step equals the adjoint direction; more steps are the content of the settling") and F into slide 14's caption.

## 4. Sources

Primer §3.1 (base, sites, write budget), §3.2 (records, delta rule), §3.3–3.4 (credit rules, v0 cap, oracle read 0.94), §3.5 (learned reader, null mass, v5 selection), §4.1–4.2 (endpoints, harm readout, 245,237 positions, ES99+), §6.4 (mixture), §10 (glossary); `docs/presentation/numbers_to_say.md` (270 cells, 392.42 process-hours); `docs/freeze_handoff_20261009_draft.md` (152.7 process-hours, 136.0 h occupancy); `docs/additional_work/R_report.md` (Option R +44.07 / +56.20).
