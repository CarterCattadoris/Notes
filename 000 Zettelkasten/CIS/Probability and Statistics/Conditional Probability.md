202601291315
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

**Conditional probability** is the probability of an event occurring given that another event has already occurred.

## Definition

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

Read as: "probability of A given B"

## Intuition

Conditional probability restricts the [[Sample Spaces|sample space]] to only outcomes where the conditioning event occurred.

## Example: Birth Months

Let:
- L = person born in a long month (31 days): {Jan, Mar, May, Jul, Aug, Oct, Dec}
- R = person born in a month with letter "R": {Jan, Feb, Mar, Apr, Sep, Oct, Nov, Dec}

**Given values:**
- $P(L) = \frac{7}{12}$
- $P(R) = \frac{8}{12}$
- $P(R \cap L) = \frac{4}{12}$ (Jan, Mar, Oct, Dec)

**Find $P(R^c \mid L)$:** probability of NO "R" given born in long month

$$P(R^c \mid L) = \frac{P(R^c \cap L)}{P(L)} = \frac{3/12}{7/12} = \frac{3}{7}$$

The 3 long months without "R": May, July, August

## Multiplication Rule

Derived from the conditional probability formula:

$$P(A \cap B) = P(B) \cdot P(A \mid B)$$

Useful for finding joint probabilities when conditional probabilities are known.

## Birthday Example

**Two people having different birthdays:**
- Person A: any birthday = $\frac{1}{365}$ (given)
- Person B different from A: $1 - \frac{1}{365} = \frac{364}{365}$

Uses the complement: $P(B^c) = 1 - P(B)$

---
### References
- Day 3 Lecture Notes (CIS321)
- [[Law of Total Probability]]
