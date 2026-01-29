202503041105
Status: #idea
Tags:[[Discrete Math (CIS375)]], [[Proofs]]

**Proof by contraposition** proves a statement by proving its [[Contrapositive|contrapositive]] instead.
To show
$$
H_{1} \land H_{2} \dots \land H_{k} \implies C_{1}
$$
it suffices to show that the contrapositive is true
$$
¬C ⇒ ¬(H_{1} ∧ H_{2} ∧ · · · ∧ Hk ) 
$$
 
1. Suppose $¬C$ is true.  
2. Show that $¬(H_{1} ∧ H_{2} ∧ · · · ∧ H_{k} )$ is true. (That is, at least one premise must be false whenever C is false.)

## Format:
Claim: Let m and n be integers. If the product mn is odd, then both m and n are odd
Proof: (by contrapositive)
- *it suffices to prove the contrapositive
	- *if its not the case that both m and n are odd, then mn is not odd*
- Suppose its not the case that both m and n are odd (NTS: mn is not odd)
$$
\dots
$$
- Thus, mn is not odd

*italicized text not required, but useful

## Examples:

Claim: Let R be an equivalence relation on set A, and let $w,z \in A$
	   If $(w,z) \not\in R$, then $[w]_{R} \cap [z]_{R} = \emptyset$

Proof:(by contrapositive)
- *it suffices to prove the contrapositive:*
	- *If $[w]_{R} \cap [z]_{R} \neq \emptyset$, then $(w,z) \in R$*
- Suppose $[w]_{R} \cap [z]_{R} \neq \emptyset$ (NTS: $(w,z) \in R$)
- Because $[w]_{R} \cap [z]_{R} \neq \emptyset$. there is some $c \in A$ such that $c \in [w]_{R}$ and $c \in [z]_{R}$, which means that $(w,c) \in R$ and $(z,c) \in R$. Because R is an equivalence relation, R is [[Symmetric]] and transitive, and hence $(c,z) \in R$ by symmetry
- Because $(w,c) \in R$ and $(c,z) \in R$, $(w,z) \in R$ by [[Transitivity]]
- Having proved the contrapositive, the original claim is true

## Related Proof Techniques
- [[Direct Proofs]]
- [[Proof by Contradiction]]
- [[Mathematical Induction]]

## Related Concepts
- [[Contrapositive]]
- [[Logic]]
- [[Equivalence Relations]]

---
### References
- [[Discrete Math (CIS375)]]