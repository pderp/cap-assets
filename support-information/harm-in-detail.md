Section 3.2 - Harm Explained in Detail

What Harm Means in This Project

Section 3.2 defines harm as the collateral damage an edit inflicts on existing knowledge. When we perturb the cap to encode a new fact, that perturbation can degrade performance on:

1. The edited prompt itself - fidelity failure
2. Paraphrases of the edited prompt - generalisation failure
3. Neighbouring facts - near-miss contamination
4. Unrelated facts - locality violation
5. Previous edits - revision failure
6. Unseen prompts - false activation

The frozen base cannot be harmed because it is never modified. Harm is specific to the cap.
The Six Axes of Harm

We evaluate harm across six axes. Each axis measures a different way an edit can damage existing knowledge.

Axis 1: Fidelity (The Edit Itself Must Succeed)

The most basic requirement: after the edit, the cap must produce the new target answer for the edited prompt. If it does not, the edit failed. Fidelity is necessary but not sufficient. A cap that achieves fidelity but corrupts everything else has simply traded one error for many.
Axis 2: Paraphrase Robustness (Generalisation)

The cap must produce the target answer not only for the exact edited prompt but for paraphrases of it. If the cap learned a surface form rather than the concept, paraphrases will fail. This is the broadest tail of the editing distribution.
Axis 3: Locality (The Edit Should Not Bleed)

The edit should only affect the edited prompt and its immediate neighbourhood. If the edit corrupts facts far from the edit site, the cap has violated locality. The control cap (random-geometry reader) fails this axis catastrophically: a single edit can corrupt unrelated knowledge across the entire model.
Axis 4: Near-Miss Contamination (Neighbouring Facts)

The edit should not corrupt facts that share a question template with the edited prompt. If the cap learned a narrow surface pattern, it may overwrite neighbouring answers. Near-miss contamination is subtle: the cap still fires, but it produces the wrong answer for prompts structurally similar to the edit site.
Axis 5: Unseen Prompts (False Activation)

The cap should not fire on prompts it was never trained to answer. If the edit causes the cap to activate on unseen prompts, it has introduced false positives. The control cap fails this axis because its random-geometry reader lacks the selectivity to distinguish trained from untrained contexts.
Axis 6: Revision (Previous Edits Must Survive)

The hardest axis. When a new edit is applied, previous edits must still produce their correct answers. If the new edit overwrites an earlier one, revision has failed. The stable cap and live caps consistently revert to old answers, while only the learned reader v5 correctly retains the newer fact.
Axis 7: Summary Table

The six axes can be summarised by which condition passes each:

- Frozen base (no cap): passes locality, near-miss, unseen, revision (cannot be harmed) but fails fidelity and paraphrase
- Control cap (random-geometry): passes fidelity but fails locality, near-miss, unseen, paraphrase
- Stable cap: passes fidelity, paraphrase, near-miss but fails revision
- Live v0 cap C1: passes fidelity, near-miss, unseen but fails paraphrase and revision
- Live v0 cap C2: passes fidelity, paraphrase, near-miss, unseen but fails revision
- Learned reader v5: passes all seven axes simultaneously

Only the learned reader v5 achieves sub-linear tail growth across all axes.
Far-From-Equilibrium: Why This Matters

The cap editing problem is fundamentally about stability under perturbation. A system at equilibrium returns to its original state after a small perturbation. A far-from-equilibrium system does not — it settles into a new state. The frozen base is at equilibrium: it ignores edits entirely. The control cap is chaotic: edits send it to unpredictable states. Only the learned reader v5 sits near the boundary where edits are absorbed without cascading damage.

The seven axes are not independent. Fidelity and paraphrase are in tension: a cap that memorises the exact prompt may fail paraphrases. Locality and near-miss are correlated: both measure bleed beyond the edit site. Revision is the hardest because it requires the cap to maintain multiple perturbations simultaneously without interference.

The learned reader v5 succeeds because it encodes edits in a structured representation that preserves locality. The random-geometry reader has no structure, so every edit corrupts everything. The stable cap retains some structure but cannot handle sequential edits. The live caps handle single edits well but degrade under revision.

The practical implication: cap editing is not a one-shot operation. Each edit must be evaluated for collateral damage across all seven axes before deployment. A cap that passes fidelity alone is not safe. The full harm profile is the cost of knowledge.
