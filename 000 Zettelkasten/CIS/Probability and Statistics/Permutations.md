202601291325
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

A **permutation** is an arrangement of objects where order matters.

## Definition

The number of ways to arrange $n$ distinct objects:

$$n! = n \times (n-1) \times (n-2) \times ... \times 1$$

## Key Properties

- Order matters
- All elements used
- No repetition

## Example: Three Envelopes

Given 3 envelopes labeled 1, 2, 3, how many ways to stack them?

**Counting:**
- Top position: 3 choices
- Middle position: 2 choices (remaining)
- Bottom position: 1 choice (remaining)

$$3! = 3 \times 2 \times 1 = 6$$

**All orderings:**
$$\Omega = \{[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]\}$$

## Partial Permutations

Choosing $r$ objects from $n$ (order matters):

$$P(n,r) = \frac{n!}{(n-r)!}$$

## Connection to [[Sample Spaces]]

Permutations define the [[Sample Spaces|sample space]] for ordering problems.

---
### References
- Day 4 - notes (CIS321)
