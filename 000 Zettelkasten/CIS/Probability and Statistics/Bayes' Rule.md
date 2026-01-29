202601291330
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

**Bayes' Rule** calculates the probability of a cause given an observed effect by inverting [[Conditional Probability|conditional probabilities]].

## Definition

Given disjoint events $C_1, C_2, ..., C_n$ that partition $\Omega$:

$$P(C_i \mid A) = \frac{P(C_i \cap A)}{P(A)} = \frac{P(C_i) \cdot P(A \mid C_i)}{\sum_{j=1}^{n} P(C_j) \cdot P(A \mid C_j)}$$

## Derivation

Starting from [[Conditional Probability]]:

$$P(C_i \mid A) = \frac{P(C_i \cap A)}{P(A)}$$

The numerator uses the multiplication rule:
$$P(C_i \cap A) = P(C_i) \cdot P(A \mid C_i)$$

The denominator uses the [[Law of Total Probability]]:
$$P(A) = \sum_{j=1}^{n} P(C_j) \cdot P(A \mid C_j)$$

## Medical Testing Example

**Setup:**
- $D$ = person has disease, $P(D) = 0.01$ (1%)
- $D^c$ = person healthy, $P(D^c) = 0.99$ (99%)
- $T_p$ = test positive, $T_n = T_p^c$ = test negative

**Test characteristics:**
- False positive rate: $P(T_p \mid D^c) = 0.05$ (5%)
- False negative rate: $P(T_p^c \mid D) = 0.002$ (0.2%)

**Question 1:** What is $P(T_p)$?

Using [[Law of Total Probability]]:
$$P(T_p) = P(D) \cdot P(T_p \mid D) + P(D^c) \cdot P(T_p \mid D^c)$$

Where $P(T_p \mid D) = 1 - P(T_p^c \mid D) = 1 - 0.002 = 0.998$

$$P(T_p) = 0.01 \times 0.998 + 0.99 \times 0.05 = 0.0595$$

**Question 2:** If a person tests positive, what's the probability they have the disease?

$$P(D \mid T_p) = \frac{P(D \cap T_p)}{P(T_p)} = \frac{P(D) \cdot P(T_p \mid D)}{P(T_p)}$$

$$P(D \mid T_p) = \frac{0.01 \times 0.998}{0.0595} = 0.1677 \approx 17\%$$

**Interpretation:** Even with a positive test, there's only a 17% chance of actually having the disease due to the low base rate (1% prevalence).

## Key Insight

Bayes' Rule "inverts" the direction of conditioning:
- Given $P(A \mid C)$ (effect given cause)
- Find $P(C \mid A)$ (cause given effect)

---
### References
- Day 4 - notes (CIS321)
- [[Law of Total Probability]]
- [[Conditional Probability]]
