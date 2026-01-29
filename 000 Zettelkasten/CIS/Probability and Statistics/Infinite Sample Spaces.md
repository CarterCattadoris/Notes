202601291310
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

An **infinite sample space** contains a countably infinite number of outcomes. Common in experiments with no fixed upper bound.

## Example: Tosses Until Heads

Question: How many coin tosses to get heads?

[[Sample Spaces|Sample space]]: $\Omega = \{1, 2, 3, 4, ...\}$ (infinite)

## Probability Distribution

For probability $p$ of heads on any toss:

$$P(n) = (1-p)^{n-1} \cdot p$$

Where $n$ = number of tosses needed.

### Derivation

- $P(1) = p$ (heads on first toss)
- $P(2) = (1-p) \cdot p$ (tails, then heads)
- $P(3) = (1-p)^2 \cdot p$ (two tails, then heads)
- $P(n) = (1-p)^{n-1} \cdot p$

## Constraints

Probability must satisfy: $0 \leq p \leq 1$

## Connection to Geometric Distribution

This is the [[Geometric Distribution]] - the probability of first success on the $n$-th trial.

---
### References
- Day 2 Lecture notes (CIS321)
