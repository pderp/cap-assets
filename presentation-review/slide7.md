# Slide 7 replacement text (Capstan, 2026-10-08)

Drop-in replacement for the slide titled "Error Predictive Coding" in the Oct 8 deck. The first paragraph is kept with a light edit; the second is rewritten because the original ("error signals propagated via skip connections") does not describe the method we used.

---

## Error Predictive Coding

Standard predictive coding is hard to scale to deep networks: the error signal has to settle layer by layer, and in a deep stack it decays or takes too many inference steps to reach the early layers.

Error predictive coding keeps the network as it is and adds one learnable error state at each transformer-block boundary on the residual stream. Training a batch has two phases:

1. **Relax.** Hold the weights fixed and adjust the error states to minimise a quadratic error penalty plus the task loss.
2. **Update.** Update each block's weights against its own local, settled target.

The local targets keep each block's weight update local, so a 12-block transformer trains without a single end-to-end backward pass. This is the recipe from the sibling repository that we re-implemented in FabricPC and used for the error-inference credit and for training the reader.

---

## Speaker note (optional, one sentence)

Our solver computes the settled errors with automatic differentiation through the graph, so our experiments test the *direction of credit* that predictive coding produces, not a biologically local hardware rule.

---

## Why the change

- The method adds no skip connections. Its defining pieces are the error state at each block boundary (`s_i = f_i(s_{i-1}) + e_i`), the relax-then-update schedule, and the detach boundaries that make each block's weight gradient local (sibling repo `docs/method.md`; our primer `docs/friday-10.02-review/README.md` §3.4 and §3.6).
- One step of relaxation from zero gives exactly the adjoint (backprop) direction after normalisation; whatever eight or thirty-two steps add is the content of the settling. That fact is what makes slides 11 and 15 interpretable, so the audience should hear it here.
- The reviewers already read the primer's statement that the solver is not a local learning rule; the slide should not contradict it.
