# Nats from first principles: turning probabilities into understandable numbers

Prepared for charlie by Capex, October 7, 2026. This guide assumes no prior knowledge of logarithms or information theory. Most examples are deliberately small illustrations. Section 10 works through an actual result from our experiments.

**A nat is a unit for measuring information or surprise on a logarithmic scale.** A likely event carries little surprise; an unlikely event carries more. In our experiments, nats also measure changes in prediction loss and differences between probability distributions.

The unit alone does not tell you which quantity was measured. Just as “five metres” could describe a height or a distance travelled, “one nat” could describe the surprise of one outcome, an increase in its prediction loss, or a divergence between two complete distributions. Those have different interpretations.

## 1. Start with a probability

A probability is a number between 0 and 1 describing how likely something is according to a particular prediction:

| Written as a percentage | Written as a probability | Plain-language reading |
| --- | ---: | --- |
| 100% | 1 | Certain under this prediction |
| 80% | 0.8 | Eight chances in ten |
| 50% | 0.5 | One chance in two |
| 10% | 0.1 | One chance in ten |
| 1% | 0.01 | One chance in a hundred |

To turn a percentage into a probability, divide it by 100. **Use 0.8, not 80, when a formula asks for an 80% probability.**

A language model assigns a probability to each possible next **token**. Tokens are pieces of text: words, parts of words, punctuation, or other character sequences. At a given position, the probabilities across its vocabulary add up to 1.

The probability is the model's prediction, not a guarantee that the prediction is correct or an independently measured chance that a statement is true. Two models can assign different probabilities to the same event.

After an outcome occurs, we can ask: **how surprising was that outcome according to the probability this model assigned to it?** That is where the calculation begins.

## 2. Why use something other than the probability itself?

We want an amount of surprise with three useful properties:

1. An event assigned probability 1 should have zero surprise.
2. Less likely events should have more surprise.
3. Surprises should add when probabilities multiply.

For the third property, imagine two independent fair coin tosses. The probability of heads followed by heads is:

```text
0.5 × 0.5 = 0.25
```

We would like the surprise of that pair to equal the surprise of the first head plus the surprise of the second. Three heads should have three times the surprise of one head.

Simply using “1 minus the probability” would not do this. It assigns surprise 0.5 to one head and 0.75 to two heads, rather than doubling it.

A **logarithm** gives us the multiplication-to-addition property. The choice of logarithm's base fixes the unit in which we measure the answer.

## 3. What a logarithm means, without assuming you know logarithms

First consider powers of 2:

```text
2¹ = 2
2² = 2 × 2 = 4
2³ = 2 × 2 × 2 = 8
```

The base-2 logarithm asks the question backward: “What power of 2 gives this number?” Therefore, the base-2 logarithm of 8 is 3.

Powers also work for negative and fractional numbers. A negative power gives a reciprocal: 2⁻¹ = 1/2. Fractional powers fill in the values between whole powers.

For **nats**, we use a different base: the mathematical constant **e**, approximately **2.71828**. The logarithm with that base is the **natural logarithm**, written **ln**.

```text
ln(x) asks: “What power of e gives x?”

ln(1) = 0        because e⁰ = 1
ln(e) = 1        because e¹ = e
ln(10) ≈ 2.302585 because e²·³⁰²⁵⁸⁵ ≈ 10
```

The constant e appears naturally in mathematics involving continuous growth and change. Using it makes many formulas convenient. You do not need to derive it to calculate nats: a scientific calculator's **ln** button uses this base.

Choosing e is a choice of information unit. It is not an assumption that our experimental harms follow an exponential distribution, or that they do or do not have heavy tails.

## 4. The basic calculation: surprise = −ln(probability)

For an event assigned probability **p**, its surprise in nats is:

```text
surprise = −ln(p)
```

The minus sign matters. For probabilities between 0 and 1, ln(p) is negative. The minus sign makes the surprise positive. An equivalent formula is:

```text
surprise = ln(1 / p)
```

This second form asks how unlikely the event was: take the reciprocal of its probability, then take the natural logarithm.

### Worked example: a 10% prediction

Suppose the model assigned the token that actually occurred a probability of 10%.

1. Convert 10% to **0.10**.
2. Calculate the reciprocal: **1 / 0.10 = 10**.
3. Calculate **ln(10) ≈ 2.302585**.

The outcome had approximately **2.303 nats of surprise under that model**.

Alternatively, a calculator gives ln(0.10) ≈ −2.302585. Change the sign to obtain the same answer.

Here are some useful reference values:

| Probability assigned to the outcome | Surprise, −ln(p) |
| ---: | ---: |
| 100% | 0 nats |
| 90% | 0.105361 nats |
| 80% | 0.223144 nats |
| 50% | 0.693147 nats |
| About 36.7879%, exactly 1/e | 1 nat |
| 10% | 2.302585 nats |
| 1% | 4.605170 nats |
| 0.0001%, or one chance in a million | 13.815511 nats |

The changes are multiplicative. Dropping from 10% to 1% adds about 2.303 nats. Dropping from 1% to 0.1% adds the same amount because both changes make the event ten times less likely.

Exactly zero probability would produce infinite surprise if that outcome occurred. The model said it was impossible. In practice, software works carefully with very small probabilities to avoid rounding them to zero unnecessarily.

For these discrete token outcomes, surprise cannot be negative. A **difference between two surprises**, however, can be negative. We will use that distinction shortly.

## 5. Why this is called loss in our experiments

If a model repeatedly assigns high probability to the tokens that actually occur, it is making good predictions by this scoring rule. If it repeatedly assigns very low probability to them, it incurs large penalties.

That penalty is called **negative log probability**, or **negative log-likelihood**, abbreviated **NLL**. For one recorded token:

```text
NLL = −ln(probability assigned to that token)
```

This is the same calculation as surprise. “Loss” emphasizes its use as a score to minimize. It does not mean money lost, a count of wrong answers, or an amount of real-world damage.

When training, an optimizer uses a loss to guide changes. When evaluating a frozen model, we can calculate the same loss without changing any weights.

For our ordinary-text evaluations, the event being scored was the next token in a saved text passage. Both the capped model and the uncapped base received the same preceding text. We looked up the probability of the recorded next token under each system.

This is distinct from deciding whether the system's single most likely answer was correct. Two models can choose the same token while assigning it different probabilities and therefore receiving different losses.

## 6. How token surprises add across a passage

Return to three independent fair coin tosses. The probability of three heads is:

```text
0.5 × 0.5 × 0.5 = 0.125
```

The surprise can be computed either way:

```text
−ln(0.125) = 2.079442 nats

−ln(0.5) − ln(0.5) − ln(0.5)
= 0.693147 + 0.693147 + 0.693147
≈ 2.079442 nats
```

The tiny discrepancy from adding the displayed rounded numbers is just rounding.

Language tokens are not independent coin tosses. Each next-token probability depends on its preceding text. Nevertheless, a passage's probability is a product of these **conditional probabilities**, so the same logarithm rule makes its total loss a sum.

For illustration, suppose a three-token continuation receives successive conditional probabilities 0.5, 0.25 and 0.1:

```text
Continuation probability = 0.5 × 0.25 × 0.1 = 0.0125

Total loss = −ln(0.0125) ≈ 4.382027 nats

Mean loss = 4.382027 / 3 ≈ 1.460676 nats per token
```

Total loss and mean loss are different quantities. Longer passages can accumulate more total loss simply because they have more tokens. A mean divides by the number of scored tokens.

This product refers to the specified continuation under the model's conditional predictions. It does not automatically describe how often a deterministic decoder, which always chooses its top-ranked token, would generate that continuation.

## 7. From a loss to a change in loss: the Δ used in our reports

Let the uncapped base assign the recorded token probability **p**, and let the capped model assign it probability **q**. We subtract their losses:

```text
Δ = capped loss − base loss
  = −ln(q) − [−ln(p)]
  = ln(p / q)
```

The symbol **Δ**, pronounced “delta,” means a change.

### Worked example: probability falls from 20% to 10%

```text
Base loss = −ln(0.20) ≈ 1.609438 nats
Cap loss  = −ln(0.10) ≈ 2.302585 nats

Δ = 2.302585 − 1.609438 ≈ +0.693147 nat
```

Or use the ratio directly:

```text
Δ = ln(0.20 / 0.10) = ln(2) ≈ +0.693147 nat
```

The positive sign says the recorded token became less likely, increasing its prediction loss. In this project's harm assay, that positive increase is the quantity called harm.

If the probability instead rises from 10% to 20%, Δ is **−0.693147 nat**. The losses themselves are still positive; the difference is negative because the cap improved this prediction score.

If the probability does not change, the ratio is 1 and Δ = ln(1) = 0.

### Relative changes versus percentage-point changes

A change from 20% to 10% loses 10 percentage points. A change from 0.02% to 0.01% loses only 0.01 percentage point. Nevertheless, both halve the probability and therefore both have Δ = ln(2).

Nats measure the logarithm of the **relative ratio**. They do not directly measure how many percentage points were lost.

## 8. Turning nats back into probabilities or ratios

The reverse of ln is **exp**, also written **e raised to a power**. On a calculator, look for **eˣ**. This is different from the **EXP** key on some calculators that merely enters scientific notation.

If you know a single outcome's loss L:

```text
probability = exp(−L)
```

If you know a loss change Δ:

```text
base probability / cap probability = exp(Δ)

cap probability = base probability × exp(−Δ)
```

A loss change alone gives a ratio, not either absolute probability. You need one of the probabilities to recover the other.

| Positive loss increase Δ | How much less likely? exp(Δ) | Fraction of previous probability remaining |
| ---: | ---: | ---: |
| 0.01 nat | About 1.01005 times | About 99.005% |
| 0.1 nat | About 1.10517 times | About 90.484% |
| 0.693147 nat, approximately ln(2) | 2 times | 50% |
| 1 nat | About 2.71828 times | About 36.788% |
| 2 nats | About 7.38906 times | About 13.534% |
| 2.302585 nats, approximately ln(10) | 10 times | 10% |
| 5 nats | About 148.413 times | About 0.674% |

For example, a **one-nat increase** takes a 20% probability down to about **7.36%**. It does not take every initial probability to 36.79%. It retains 36.79% **of whatever probability was there before**.

These ratio interpretations apply directly to an individual **Δ**. They must not be transferred unchanged to every other quantity measured in nats, particularly KL or an average across many positions.

## 9. KL: another calculation that also uses nats

The preceding calculation followed one recorded outcome. **Kullback–Leibler divergence**, abbreviated **KL**, considers all possible outcomes.

For our direction of comparison, it asks: if we average the log probability ratios using the **base model's probabilities as weights**, how much do the complete distributions differ?

Here is an illustrative two-outcome model:

| Possible next token | Base probability p | Cap probability q | ln(p/q) | Base-weighted contribution p × ln(p/q) |
| --- | ---: | ---: | ---: | ---: |
| A | 0.8 | 0.6 | +0.287682 | +0.230146 |
| B | 0.2 | 0.4 | −0.693147 | −0.138629 |

Calculate each row's probability ratio, take its natural logarithm, multiply by its base probability, then add the contributions:

```text
KL(base ∥ cap)
= 0.8 × ln(0.8 / 0.6) + 0.2 × ln(0.2 / 0.4)
≈ 0.091516 nats
```

The displayed rounded contributions give a slightly different final decimal if added directly; the answer above uses unrounded values.

If the recorded token is A, its actual Δ is +0.287682. If it is B, its actual Δ is −0.693147. In both cases, the KL for this position remains 0.091516 because the full distributions are the same.

Although some contributions are negative, their complete probability-weighted sum is nonnegative mathematically. KL is zero for identical distributions. Reversing the comparison generally changes it: this example gives **KL(cap ∥ base) ≈ 0.104650**, a different value.

For the real GPT-2 experiment, this sum runs over all **50,257 vocabulary tokens** at each scored prefix. We then average the position-level KL values over the chosen text inventory.

**KL of 0.001 nat does not mean 0.1% incorrect answers, or a 0.1% drop in each token's probability.** A KL value summarizes a whole distribution; it does not specify a unique change to any one token.

The same point applies to a model's overall average KL: the average alone does not locate which prefixes changed, how many changed, or the size of the largest change.

## 10. An actual experiment, converted step by step

In the learned-reader zsRE run with realization 0 and order 100, after 1,000 edits, one recorded token was **` As`**, including its leading space. The saved loss values at that location were:

| System | Saved loss in nats |
| --- | ---: |
| Uncapped base | 10.4337923808 |
| Base with the learned cap | 19.6960598445 |

Recover the probabilities by undoing the negative logarithm:

```text
Base probability = exp(−10.4337923808)
                 ≈ 0.0000294213

Cap probability  = exp(−19.6960598445)
                 ≈ 0.00000000279325
```

Now subtract the losses:

```text
Δ ≈ 19.6960598445 − 10.4337923808
  ≈ 9.262267 nats
```

Convert that loss change into a ratio:

```text
exp(9.262267...) ≈ 10,533
```

The cap made this recorded token about **10,533 times less likely**. Both probabilities were already very small. This is not evidence that the uncapped model's top-choice prediction had been correct and the cap changed it to an incorrect answer.

KL at the same position was approximately **6.744336 nats**, a different number because it included the probabilities of every vocabulary token. These are actual saved measurements, documented in the [slide-12 explanation](slide-12-probabilities-fidelity-and-rare-harm.md) and its linked verification record.

## 11. Why an average needs its own interpretation

Suppose, purely as an illustration, that 999 scored positions have Δ = 0 and one has Δ = 10. The mean is:

```text
(999 × 0 + 1 × 10) / 1,000 = 0.01 nat per position
```

The average is small even though one token became about exp(10), or **22,026 times less likely**. None of the positions actually had Δ = 0.01.

Negative changes can also cancel positive changes in a signed mean. A change of +1 nat at one position and −1 nat at another averages to zero. That does not mean neither prediction changed.

For a mean signed Δ, exponentiating the mean produces the **geometric mean** of the base-to-cap probability ratios. A geometric mean multiplies ratios and takes the appropriate root, rather than adding them. It is not the ordinary arithmetic mean of those ratios, and does not identify the change at any particular token.

Similarly, exp(−mean NLL) gives the geometric mean of the assigned token probabilities, not their arithmetic mean. If you encounter **perplexity**, it is exp(mean NLL) when the loss is measured in nats per token. Perplexity is a related summary, not the percentage of incorrect predictions.

This is why our reports also examine maxima, frequencies above a threshold, and the average severity of the worst portion of the loss-change distribution.

## 12. Nats and bits are different units for the same information

If we used a base-2 logarithm rather than a natural logarithm, surprise would be measured in **bits**:

```text
surprise in bits = −log₂(p)
surprise in nats = −ln(p)
```

For one fair coin toss, an outcome has probability 0.5. Its surprise is **1 bit**, or approximately **0.693147 nat**.

The conversions are:

```text
nats = bits × ln(2) ≈ bits × 0.693147
bits = nats / ln(2) ≈ nats × 1.442695
```

Thus one nat is approximately **1.442695 bits**. Converting units does not change which prediction is better or how many times a probability changed.

This use of “bit” measures information. It does not say that a particular token occupies that many physical bits in a file. Actual file encodings involve additional choices and overhead.

On calculators, **log** often means base 10, whereas **ln** means base e. Using the wrong button changes the unit. In Python's standard `math` module, `math.log(x)` is the natural logarithm; `math.log2(x)` is base 2 and `math.log10(x)` is base 10.

## 13. Where entropy and cross-entropy fit

These terms also use the same building blocks, so they can look deceptively similar in papers.

**Entropy** is average surprise when outcomes are weighted according to the same distribution whose surprise we calculate. For probabilities p:

```text
entropy = sum over outcomes of p × [−ln(p)]
```

For the 80%/20% distribution above, this is about **0.500402 nats**.

**Cross-entropy** uses one distribution's probabilities to weight another distribution's surprise. With p as the reference distribution and q as the model being evaluated:

```text
cross-entropy = sum over outcomes of p × [−ln(q)]
```

Using p = [0.8, 0.2] and q = [0.6, 0.4] gives approximately **0.591919 nats**. Their difference is KL:

```text
cross-entropy − entropy
≈ 0.591919 − 0.500402
≈ 0.091516 nats
```

Again, calculations use the unrounded numbers. Averaging observed next-token NLL is often called empirical cross-entropy: it uses the recorded outcomes to score the predictions.

You do not need these extra formulas to calculate one token's surprise. Their purpose here is to show that **a nat is a common unit for several related quantities**, rather than the name of one specific test.

## 14. How the computer obtains the probabilities

Internally, the language model first produces a numerical score for each possible next token, called a **logit**. A conversion called **softmax** exponentiates these scores and divides by their total, giving probabilities that add up to 1.

The program does not need to print every probability, round it, and then take its logarithm. It can compute **log probabilities** directly using a numerically stable calculation. This matters for extremely unlikely tokens: a small displayed probability might round to zero even though the model assigned it a positive value.

Our evaluation code calculates normalized log probabilities, takes the negative log probability of the recorded token for NLL, subtracts losses for Δ, and sums probability-weighted log ratios for KL. Tiny negative KL values attributable to floating-point roundoff are treated as zero; substantial negatives are rejected. The mathematical definition remains nonnegative.

“Stable numerical calculation” changes how the computer evaluates the formula; it does not change the information unit. This explanation and its arithmetic checks require no model retraining or GPU work.

## 15. Reading the one-nat bound in slide 24

The probability-mixture experiment retained a base contribution of ρ = exp(−1), approximately 0.367879:

```text
mixture probability = ρ × base probability
                    + (1−ρ) × cap probability
```

The cap's contribution cannot be negative. Consequently:

```text
mixture probability ≥ exp(−1) × base probability

base probability / mixture probability ≤ e

ln(base probability / mixture probability) ≤ 1 nat
```

This is a guarantee about the **increase in token loss**, at the same prefix relative to the same base. It is not a guarantee that the token's total loss is below one nat. A token could have base loss 10 and mixture loss 10.8: the increase is only 0.8 even though both losses are much larger than one.

Nor does the bound guarantee a correct answer or a mean KL below the much stricter registered threshold of 0.001. The [slide-24 explanation](slide-24-experimental-lessons-and-open-questions.md) describes the measured benefits and remaining failures.

## 16. A short recipe to keep beside the slides

| What you want to know | Calculation | How to read it |
| --- | --- | --- |
| Surprise of an outcome assigned probability p | −ln(p) | Bigger means the model considered this outcome less likely. |
| Probability from a single outcome's loss L | exp(−L) | Recovers the probability that produced that loss. |
| Change from base probability p to cap probability q | ln(p/q) | Positive means the recorded outcome became less likely. |
| Probability-reduction factor from a loss increase Δ | exp(Δ) | For example, +1 nat means about 2.72 times less likely. |
| KL from two complete distributions | Sum p × ln(p/q) over all outcomes | Measures distributional change in the specified direction. |
| Mean loss or mean Δ | Add values and divide by scored positions | Describes an average, not the largest or every individual change. |
| Convert nats to bits | Divide by ln(2) | Changes the unit, not the underlying result. |

Before interpreting any reported value, ask: **nats of what, for which outcomes, relative to which reference, and averaged over what?** Those four questions prevent most of the confusion.

### Project sources and checks

- [Slide-12 explanation](slide-12-probabilities-fidelity-and-rare-harm.md): actual saved token example, full-validation population, Δ and KL thresholds.
- [Saved verification for that example](../../pc_cap/logs/presentation/slide-12-fidelity-20261006/verification.json): unrounded losses, probabilities, ratio and provenance.
- [Full-validation implementation](../../pc_cap/scripts/r1_68f_full_validation.py): token losses, KL direction and roundoff handling.
- [Bounded-correction implementation](../../pc_cap/aw/bounded.py): normalized log probabilities and mixture calculations.
- [Slide-24 explanation](slide-24-experimental-lessons-and-open-questions.md): experimental interpretation of the one-nat bound.

Illustrative calculations were independently checked with Python's standard mathematical functions. The historical example was checked against its existing saved verification record. No new experimental result is introduced here.
