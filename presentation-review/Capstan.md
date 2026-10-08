# Capstan review of `Predictive_Coding_Cap_Experiments.pdf`

Reviewed 2026-10-08 (file dated Oct 8 05:21, 24 slides, Google Slides export). Every number on the deck was checked against the frozen record in `pc_cap/docs/` (Stage-4 triplet report, `additional_work_report.md` and the lane reports it cites). Every hyperlink was extracted from the PDF and checked. The QR code could not be decoded here (no decoder installed), so its target is unverified.

**Verdict.** All numbers on slides 9, 10, 11, 12, 14 and 15 match the record exactly. Nothing on the deck over-claims. The problems are (1) one wrong hyperlink, (2) two technical statements about predictive coding that do not describe what we actually ran, (3) several slides that cannot be understood without context the deck never gives, and (4) a few strong results that are missing. Items in §1 should be fixed before the talk; §2 and §3 are recommendations.

---

## 1. Must fix

### 1.1 Slide 5: the CounterFact link points to the wrong paper
The CounterFact link goes to arXiv 2502.11008, which is **CounterBench** (Chen et al. 2025, "Evaluating and Improving Counterfactual Reasoning in LLMs"). We did not run CounterBench; Capex's long deck says so explicitly. The dataset we used is **CounterFact**, introduced in Meng et al. 2022, "Locating and Editing Factual Associations in GPT" (ROME), arXiv **2202.05262**. The zsRE link (1706.04115) and the MQuAKE link (2305.14795) are correct.

### 1.2 Slide 7: "Error predictive coding ... propagated via skip connections" is not what the method is
The sibling repository and our implementation define the method as follows: one error tensor is added at each transformer block boundary on the residual stream (`s_i = f_i(s_{i-1}) + e_i`); the errors are relaxed by gradient descent on a quadratic energy plus the task loss while the weights are held fixed; then each block's weights are updated against detached local targets. There are no added skip connections. The thing that makes deep training work is the detach boundaries that keep each block's weight gradient local, plus the staged relaxation budget. Suggested replacement for the second paragraph:

> Error predictive coding adds a learnable error state at each block boundary of the residual stream. The network first relaxes those error states against the task loss with the weights fixed, then updates each block's weights against its own local target. That keeps weight updates local while still letting a deep transformer train.

The first paragraph (standard PC struggles in deep networks because the error signal decays across many layers) is an acceptable lay statement.

### 1.3 Slide 6: do not imply our runs realised local learning
The last sentence says PC "allows for locally updating the weights of each layer ... without needing to propagate errors all the way through the entire network". As a description of the paradigm it is fine, but a listener will assume our experiments did that. They did not: the FabricPC solver computes the error gradient by autodiff through the whole graph, and the primer we gave the reviewers says in so many words that "this is not a local or biologically plausible learning rule". Add one clause, for example: "(our implementation computes the settled errors with autodiff through the graph; it tests the credit *direction* that PC produces, not a local hardware rule)". This matters because Kenric Nelson and Matt Iklé both read the primer and will notice.

### 1.4 Slide 18: the sentence is unintelligible without the experiment it refers to
"An adjoint control used 53–58% of its offered budget" is lifted from Capex's long deck, where two earlier slides set it up. On its own nobody will know what budget, what control, or why it matters. Suggested rewrite:

> Eight settling steps raised own-prompt retention (51.5% → 53.4% on zsRE) at about twice the learning time. We gave an adjoint control the same operation budget, but its stopping rule and rollback meant it only used 53–58% of it. So we cannot yet say whether the gain comes from the direction of the PC credit or simply from more compute.

### 1.5 Slide 1 and 2: talk title versus submitted title
"Thriving in the Extremes: Active Inference in Non-equilibrium Systems" is the satellite's name, not the talk's. The programme lists the talk under the submitted title, *Coupled Active Inference on a Frozen Transformer Prior: A Risk-Aware Residual Agent for Non-Equilibrium Regimes*. Our outline of 18 Sep recommended keeping that title visible with a subtitle. Suggest: slide 1 keeps the satellite name but labelled as the session ("CSS2026 satellite: Thriving in the Extremes ..."), and slide 2 adds the submitted title as a sub-line, or slide 3 says "submitted as: ...". Otherwise people matching the programme to the room will be confused, and the drift you acknowledge on slide 4 looks larger than it is.

---

## 2. Number check (all verified)

| Slide | Claim | Record | Status |
|---|---|---|---|
| 9 | stable v0 zsRE 66.68% / 18.56%; learned 96.03% | triplet report: v0_stable RET-ES 0.660/0.6474/..., RET-GS 0.1856; learned RET-GS 0.96033 | match |
| 9 | CounterFact 100% / 0% / 67.80%; MQuAKE 100% / 0% / 71.56% | v0_stable 1.0/0.0 all realizations; learned 0.678, 0.71556 | match |
| 10 | all 45 learned-reader cells exceed mean KL 0.001 | `additional_work_report.md` line 11; Stage-4 report | match |
| 10 | CounterFact learned-vs-v0 inconclusive, locality failed | triplet report: locality 48/50 in realization 2 | match |
| 11 | 98.3 / 98.3 / 80.7 / 80.3% paraphrase; 316 / 426 / 297 / 359 s; 9.26 / 12.27 / 11.74 / 12.23 nats | PC-v1 report: RET-GS 0.983333/0.983333/0.806667/0.803333; whole-process seconds 316.111/426.036/297.33/359.424; largest maximum 9.26227/12.27/11.7442/12.2254 | match |
| 12 | BP 97.3/99.0/97.7, ePC 94.7/97.0/98.0 (zsRE); BP 81.0/80.0/83.5, ePC 56.8/77.8/66.0 (CF); 300 updates; 3.35M params; adjoint acquisition | PC-reader report per-cell table; 3,348,228 parameters; "acquisition uses adjoint in every arm" | match |
| 14 | 1.619 → 0.542 and 1.925 → 0.581 nats; ten memories, 2 datasets × 5 orders, 300 edits | HT-17 report | match |
| 15 | 51.5 / 53.4 / 56.5%; 13.1 / 13.1 / 12.2%; 5.7 / 10.2 / 25.4 min; 50M ePC base, v0 cap, 3 realizations, order 100, 1,000 edits | PC-controls report SE-E rows: 0.515333/0.534/0.565; 0.130667/0.131/0.122; learning s/cell 341.2/614.0/1524.9 | match |
| 18 | 53–58% of offered budget | `additional_work_report.md` line 103 (PC-matched control) | match |
| 19 | κ-loss pilot missed its success rule | report §"Legacy κ pilot": both κ arms fail the retention floor; no tail reduction beyond seed spread | match |

Two captions are correct but incomplete and should say so on the slide:
- **Slide 11** is one exposed realization (r0, order 100, 300 edits). The report states "no independent realization interval". Add "one realization" to the caption so the 316 s vs 426 s comparison is not read as a population result.
- **Slide 15** shows only the error-inference rows. The paired adjoint baseline at every depth gets the same 51.5% / 13.1% in 4.6 min, and one-step error credit is *algebraically identical* to adjoint credit. The slide also omits that harm rises with depth (mean loss increase on ordinary text 0.00145 → 0.00157 → 0.00221 nats; ES99+ 0.156 → 0.167 → 0.236). "Bought retention at a cost" is true, but the cost is time *and* harm, and the paraphrase column already shows the generalisation did not improve. Suggest adding a "Mean Δ loss (ordinary text)" column and an adjoint row.

---

## 3. Recommendations on content and order

### 3.1 Define the objects before using them
The deck never says what a "cap" is, what "stable v0", "learned reader", "v5 reader" or "the mixture" are, or what "retention" measures. Slide 8 ("fixed machinery and an empty correction memory") is the closest it comes. One slide after slide 7 would carry the talk: frozen GPT-2 small (124M); a 3.35M-parameter reader that decides whether a prompt matches a stored correction and can abstain; write vectors at three residual sites; corrections taught one at a time and tested by original prompt (own-prompt retention), by paraphrase (paraphrase retention), and on 245k positions of ordinary text (harm). "Stable v0" = the first-month radius-gated activation memory with a fixed schedule; "learned reader" = the Stage-4 trained reader; "v5" = the selected learned-reader checkpoint; "mixture" = the cap's output distribution mixed with the frozen base's at base weight e⁻¹, which bounds any per-token loss increase at one nat at the same prefix. The abstract's two-interface diagram or Capex's long-deck figures (`assets/presentation-materials/deck_v4/long_deck_v1_assets/figures/`) can be reused.

### 3.2 Slide 14 uses "the mixture" five slides before slide 19 explains it
Either move the one-line definition above onto slide 14, or move slide 14 to sit after slide 19 ("A simple bound was useful"), where it becomes the evidence for that lesson.

### 3.3 Results that are missing and are among the strongest we have
- **Independent replication (Option R).** Over four subject realizations the learned reader beats the random-geometry reader by 44.1 percentage points of paraphrase retention on zsRE and 56.2 on CounterFact (t(3) sensitivity intervals 41.6–46.6 and 54.2–58.2). This is the cleanest support for "Retrieval is central" (slide 17) and is currently absent.
- **Upper-layer interface (AW-L).** Slide 17 says the restriction "did not provide the hoped-for benefit" but gives no number. The record: writing only at the last site keeps paraphrase retention within 0.67 points but raises mean ordinary-text loss increase by 2.64–4.37× in all twelve paired comparisons; reading only upper layers loses CounterFact paraphrases. One line with the ratio makes the lesson concrete.
- **Cost of the PC-trained reader.** Slide 12 says "mixed outcomes" but omits the cost that makes it mixed: measured ePC training time was 95.8–102.1× BP (23.4–24.6 h vs about 15 min per seed). Add it to the caption.
- **Scale and compute.** Nowhere does the deck say GPT-2 small / 124M parameters, 270 confirmatory cells, 392 process-hours for the main study plus 153 for the supplements, all on one local GPU. Reviewers asked about scale on Oct 2; one line on slide 8 or 11 answers it and pre-empts "does this transfer to large models" (answer: not established).

### 3.4 Slide 13 (tail figure)
Correct and well chosen. Two notes. The y-axis label and the boxed sentence do not say which quantity the exponential was fitted to; say "excess over the 0.01-nat threshold" or drop "saved exponential fit" from the legend. And keep to the agreed wording from DEC-081a if asked: these are fitted finite-range shapes, not complexity classes, not infinite variance, not an entropy measurement. The slide as written respects that.

### 3.5 Slide 3 (agents)
I can confirm "Capstan: Claude Fable 5.1". I cannot verify the Capex model name or the Derp Peoples / Omega description; please check those yourself. "Agentic assistance was used with planning, reviewing, and running the experiments" is accurate.

### 3.6 Slide 10 wording
"Registered mean-KL preservation benchmark of 0.001" needs units and object: "mean KL ≤ 0.001 nats per token on ordinary text". Also consider saying what the harm looks like in one phrase (rare, concentrated: a few positions per ten thousand carry most of the loss increase), since that is the link to the "extremes" theme.

### 3.7 Slide 20
The Markov-blanket paragraph is exactly the DEC-081a position and reads well. Consider ending it with the concrete next step from Capex's deck ("specify the states, specify the interfaces, test the asserted property"), since that is what the post-conference collaboration would actually do.

---

## 4. Links and the QR code

| Slide | Link | Checked |
|---|---|---|
| 3 | github.com/pderp/pc_cap/blob/master/docs/pc_cap_month_plan_readable.pdf | file is tracked and the public page returns 200 |
| 3 | earthland.ai/.../Active_Inference_in_the_Extremes_Abstract_charlie_derr.pdf | returns 200; title is the submitted title (§1.5) |
| 3 | github.com/singnet/Omega | present |
| 5 | zsRE → arXiv 1706.04115 | correct (Levy et al. 2017) |
| 5 | MQuAKE → arXiv 2305.14795 | correct (Zhong et al. 2023) |
| 5 | CounterFact → arXiv 2502.11008 | **wrong paper** (CounterBench); use 2202.05262 |
| 21, 23 | bgilabs.ai, earthland.ai, singularitynet.io, trueagi.io | present |
| 1, 24 | QR code | not decoded here; the canonical location is https://earthland.ai/ccs/, which links the Google Slides deck (confirmed Oct 8). Please confirm the QR resolves to that page or that deck |

The PDF under review lives at `/home/derp/cap/` outside both repositories; `assets/presentation-materials/deck_v5/` holds only a short `raw_content` note so far. Slide 5's CounterFact link was corrected by the lead on Oct 8 after this review; the corrected slide-7 text is in `slide7.md` beside this file.

---

## 5. Minor

- Slide 6, last sentence has no full stop.
- Slide 1 and 24: the ASCII arrow "—--------------->>>>>" looks like a rendering glitch; a plain "→" or nothing reads better.
- Slide 9 and 11 have no title. Suggested: "Paraphrase retention after 1,000 edits (300 for MQuAKE)" and "Changing only the acquisition credit (one realization, 300 edits)".
- Slide 15 "Legacy 50M ePC base" is correct (the August–September study base) but "legacy" will puzzle the room; "first-month 50M ePC-distilled base" is clearer.
- Slide 11 column "Acquisition process" is whole-process seconds (construction, lease, startup and the 300 acquisitions). "Process time per cell" is more honest than "acquisition process".
- The deck has two title slides and 24 pages for a Session 3 slot of unknown length; the record never established your individual speaking time. If it is 15–20 minutes, slides 4, 6 and 7 can be merged and slides 16–19 can become one.

## 6. What I did not check
The QR code target (no decoder available); the model names on slide 3 other than my own; the speaker notes, if any, since the export carries none.
