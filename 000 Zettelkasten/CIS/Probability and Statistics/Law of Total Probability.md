202601291320
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

The **Law of Total Probability** expresses the probability of an event as a weighted sum of [[Conditional Probability|conditional probabilities]] over a partition of the [[Sample Spaces|sample space]].

## Definition

Given disjoint events $C_1, C_2, ..., C_n$ that partition $\Omega$:

$$P(A) = \sum_{i=1}^{n} P(A \mid C_i) \cdot P(C_i)$$

## Expanded Form

$$P(A) = P(A \mid C_1)P(C_1) + P(A \mid C_2)P(C_2) + ... + P(A \mid C_n)P(C_n)$$

## Requirements

The conditioning events must:
1. Be **mutually disjoint**: $C_i \cap C_j = \emptyset$ for $i \neq j$
2. **Cover the sample space**: $C_1 \cup C_2 \cup ... \cup C_n = \Omega$

## Derivation

From the definition of conditional probability:

$$P(A \mid C_i) = \frac{P(A \cap C_i)}{P(C_i)}$$

Therefore:
$$P(A \cap C_i) = P(A \mid C_i) \cdot P(C_i)$$

Since $A = (A \cap C_1) \cup (A \cap C_2) \cup ... \cup (A \cap C_n)$ and these are disjoint:

$$P(A) = \sum_{i=1}^{n} P(A \cap C_i) = \sum_{i=1}^{n} P(A \mid C_i) \cdot P(C_i)$$

## Use Cases

- When direct calculation of $P(A)$ is difficult
- When conditional probabilities are easier to compute
- Foundation for [[Bayes' Rule]]

---
### References
- Day 3 Lecture Notes (CIS321)
