202503041130
Status: #idea
Tags:[[Discrete Math (CIS375)]], [[Proofs]]

**Proof by contradiction** assumes the negation of what you want to prove, then derives a [[Contradiction|contradiction]].

To show $$H1 ∧ H2 ∧ · · · ∧ Hk ⇒ C$$ 
it suffices to show that  
$$(H1 ∧ H2 ∧ · · · ∧ Hk ∧ ¬C ) ⇒ False  $$
1. Suppose $H_{1}, H_{2}, . . . , H_{k}$ and $¬C$ are all true.  
2. Show that a contradiction follows.  (Any contradiction works, but they usually have form $q ∧ ¬q$)

Important logical equivalence:
$$
\neg p \to False ≡ P
$$
Important special case:
$$(h ∧ ¬c) → False ≡ ¬(h ∧ ¬c) ≡ ¬h ∨ c ≡ h → c$$

## Format:
Claim: Let m and n be integers. If the product mn is odd, then both m and n are odd.  
Proof: (by contradiction)  
- Suppose that mn is odd and that it’s not the case that both  
- m and n are odd. (NTS: a contradiction.)
$$...  $$
- Because negating the desired conclusion leads to a contradiction, the original claim must be true

## Examples:

Claim: Let n be an integer. If n is even, then n is not odd

Proof:(by contradiction)
- Suppose that n is even ad that it is not the case that n is not odd (NTS: a contradiction)
- Because n is even, there is an integer k such that $n = 2k$
- Because its not the case that n is not odd, n must be odd, and hence there is an integer j such that $n = 2j + 1$
- Therefore, $2k = 2j+1$, which (by algebra) means that $2k-2j = 1$, and hence $k - j = \frac{1}{2}$
- However, k and j cannot both be integers when $k-j=\frac{1}{2}$ contradicting earlier statements that they are integers.  
- Because negating the desired conclusion leads to a contradiction, the original claim must be true.

## Related Proof Techniques
- [[Direct Proofs]]
- [[Proof by Contraposition]]
- [[Mathematical Induction]]

## Related Concepts
- [[Contradiction]]
- [[Logic]]

---
### References
- [[Discrete Math (CIS375)]]