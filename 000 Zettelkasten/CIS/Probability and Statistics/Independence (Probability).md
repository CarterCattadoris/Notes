202601291335
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

Two events are **independent** if the occurrence of one does not affect the probability of the other.

## Definition

Events $A$ and $B$ are independent if:

$$P(A \mid B) = P(A)$$

Equivalently:
$$P(B \mid A) = P(B)$$

## Multiplication Rule for Independent Events

If $A$ and $B$ are independent:

$$P(A \cap B) = P(A) \cdot P(B)$$

## Equivalent Definitions

If $A$ and $B$ are independent, then:

1. $P(A \mid B) = P(A)$
2. $P(B \mid A) = P(B)$
3. $P(A \cap B) = P(A) \cdot P(B)$

## Complement Property

If $A$ and $B$ are independent, then $A^c$ and $B$ are also independent:

$$P(A^c \mid B) = 1 - P(A \mid B) = 1 - P(A) = P(A^c)$$

## Derivation

From [[Conditional Probability]]:
$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

If $P(A \mid B) = P(A)$, then:
$$P(A) = \frac{P(A \cap B)}{P(B)}$$
$$P(A \cap B) = P(A) \cdot P(B)$$

## Contrast with Mutual Exclusivity

| Property | Mutually Exclusive | Independent |
|----------|-------------------|-------------|
| Definition | $A \cap B = \emptyset$ | $P(A \mid B) = P(A)$ |
| Joint probability | $P(A \cap B) = 0$ | $P(A \cap B) = P(A) \cdot P(B)$ |
| Can both occur? | No | Yes |

## Key Insight

Independence means knowing $B$ occurred tells you **nothing** about whether $A$ occurred.

---
### References
- Day 4 - notes (CIS321)
- [[Conditional Probability]]
