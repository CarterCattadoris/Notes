202601291305
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

**Products of sample spaces** combine multiple independent experiments into a single [[Sample Spaces|sample space]] using the Cartesian product.

## Definition

For experiments with sample spaces $\Omega_1$ and $\Omega_2$:

$$\Omega_f = \Omega_1 \times \Omega_2$$

## Example: Two Coin Tosses

Each coin: $\Omega = \{H, T\}$

Combined sample space:
$$\Omega_f = \{H, T\} \times \{H, T\} = \{(H,H), (T,T), (H,T), (T,H)\}$$

**Probabilities:**
- $P(H,H) = \frac{1}{4}$
- $P(T,T) = \frac{1}{4}$
- $P(H,T) = \frac{1}{4}$
- $P(T,H) = \frac{1}{4}$

## Example: Two Dice

Each die: $\Omega = \{1, 2, 3, 4, 5, 6\}$

$$\Omega_f = E_1 \times E_2 = \{1,2,3,4,5,6\} \times \{1,2,3,4,5,6\}$$

Total outcomes: $6 \times 6 = 36$

Examples: $(1,3), (1,4), (2,3), (2,2), ...$

## Counting Principle

For $n$ independent experiments with $|\Omega_1|, |\Omega_2|, ..., |\Omega_n|$ outcomes:

$$|\Omega_f| = |\Omega_1| \times |\Omega_2| \times ... \times |\Omega_n|$$

---
### References
- Day 2 Lecture notes (CIS321)
