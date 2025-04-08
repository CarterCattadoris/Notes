202502251110
Status: #idea
Tags:[[Relations]]

## Proof 1
Claim: Let S and T be relations on set Q. If $S \subseteq T$ and T is irreflexive, then $S^{-1}$ is irreflexive

Proof:(direct)
- Suppose $S \subseteq T$ and T is irreflexive
- NTS: $S^{-1}$ is irreflexive, which means that for all $x \in Q$, $(x,x) \not\in S^{-1}$
- Consider an arbitrary $a \in Q$ (NTS: $(a,a) \not\in S^{-1}$)
- Because T is irreflexive, $(a,a) \not\in T$
- Because $S \subseteq T$  and $(a,a) \not\in T$, $(a,a) \not\in S$
- Thus, $(a,a) \not\in S^{-1}$
- Because a was an arbitrary element of Q, $S^{-1}$ is irreflexive

## Proof 2
Claim: Let S and T be relations on set W. If S and T are both symmetric, then S-T is symmetric

Proof:(direct)
- Suppose S and T are both symmetric
- NTS: S-T is symmetric, which means that for all $x,y \in W$, if $(x,y) \in S-T$, then $(y,z) \in S-T$
- Consider arbitrary $a,b \in W$ such that $(a,b) \in S-T$ (NTS: $(b,a) \in S-T$)
- By definition of S-T, $(a,b) \in S$ and $(a,b) \not\in T$
- Because $(a,b) \in S$ and S is symmetric, $(b,a) \in S$
- Because $(a,b) \not\in T$ and T is symmetric, $(b,a) \not\in T$
- Thus, $(b,a) \in S-T$
- Because a,b were arbitrary elements of W, S-T is symmetric

## Proof 3
Claim: Let S and T be relations on set G. If S is antisymmetric, then $S^{-1} \cap T$ is antisymmetric

Proof:(direct)
- Suppose S is antisymmetric. (NTS: $S^{-1} \cap T$ is antisymmetric, which means for all $x,y \in Q$, if $(x,y) \in S^{-1} \cap T$ and $(y,x) \in S^{-1} \cap T$, then x=y)
- Consider arbitrary $a,b \in S^{-1} \cap T$
- By definition of $S^{-1} \cap T$,
	- $(a,b) \in S^{-1}$ and $(b,a) \in S^{-1}$
- By definition of $S^{-1}$
	- $(b,a) \in S^1$ and $(a,b) \in S$
- Because S is antisymmetric, a=b
- Because a,b were arbitrary elements of Q, $S^{-1} \cap T$ is antisymmetric

