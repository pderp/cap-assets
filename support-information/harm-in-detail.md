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
