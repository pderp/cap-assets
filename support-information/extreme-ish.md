# How the Three Datasets Deal with Extremes (Far from Equilibrium)

## Overview

The cap project tests a knowledge-editing system built on a frozen GPT-2 small model. A small adaptive layer sits atop the sealed base and is perturbed once per fact in a continuous stream of edits. Three datasets supply those edits, each creating a different kind of non-equilibrium pressure on the system.

## 1. Shared Non-Equilibrium Structure

- Frozen prior: GPT-2 base is sealed; all adaptation happens in the cap.
- Small adaptive layer: low-dimensional perturbation applied once per fact.
- Continuous driving: edits arrive one at a time in fixed order (10^0 to 10^4 facts). No steady state.
- Path dependence: edit order changes the trajectory through weight space.
- Rare-harm tail: most edits are benign; a small fraction causes outsized damage.

## 2. zsRE — Zero-Shot Relation Extraction

Single-relation edits tested under paraphrase pressure. No locality or multi-hop controls. Extremes manifest as generalisation failures under paraphrase.

## 3. CounterFact — Counterfactual Fact Substitution

Counterfactual edits with rich control prompts probing seven axes: fidelity (immediate and end-of-stream), paraphrase robustness, locality (unrelated facts), near-miss (neighbouring facts), unseen prompts, and revisions. Extremes manifest as multi-dimensional failure modes.

## 4. MQuAKE — Multi-hop Question Answering for Knowledge Editing

Multi-hop reasoning chains where a single edit must propagate through connected questions. Chain length amplifies per-hop failure probability. Extremes manifest as cascade failures through reasoning chains.

## 5. Comparative Summary

| Dimension | zsRE | CounterFact | MQuAKE |
|---|---|---|---|
| Edit granularity | Single relation | Single counterfactual | Single fact (multi-hop) |
| Locality control | None | Explicit | Implicit |
| Unseen-prompt | No | Yes | Yes |
| Revision | No | Yes | Yes |
| Tail shape | Narrow: paraphrase | Broad: 7 axes | Amplified: chain-length |
| Stream sensitivity | Linear | Linear, wider tail | Super-linear |

## 6. The Far-From-Equilibrium Connection

- zsRE measures responsiveness — does the system move to the new state?
- CounterFact measures selectivity — does it move only the target?
- MQuAKE measures coherence — does a local change propagate correctly?

The rare-harm tail is the fraction of edits that push the system into failure. The goal is to measure whether that tail grows sub-linearly (graceful) or super-linearly (catastrophic) with stream length.

---

Written 2026-10-09. Based on review of cap/assets/support-information/ and cap/pc_cap/ documentation.