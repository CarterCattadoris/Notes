1. For each of the following statements, determine whether or not it is true. For each statement that is false, provide a concise and compelling explanation of why it’s false.

	 1. $\{\{a, b, c\}, \{d, g\}, \{b, f, e\}, \{h\}\}$ is a partition of $\{a, b, c, d, e, f, g, h\}$.
		 1. False, element b appears twice making it not a partition
	12. {1, \{3, 4\}, \{5\}, \{2\}\}$ is a partition of $\{1, 2, 3, 4, 5\}$.
		12. lse, the element 1 is not a set therefore making it not a valid partition
	23. {Z+, \{−1, −2\}, \{0, −3\}, \{w ∈ Z : w < −4\}\}$ is a partition of Z.
		13. lse, doesn't include -4 ($w <-4$ not $w \leq -4$)
	34. {\{2n : n ∈ N\}, \{2n + 1 : n ∈ Z+\}, \{n ∈ N : n ∈ Z−\}\}$ is a partition of Z.
		14. lse, the third set is empty, and the remaining sets dont cover negative numbers and 1


2. For each of the following relations, determine whether or not it is an equivalence relation and support your answer as follows:
- If it’s an equivalence relation, give its equivalence classes.
- If it’s not an equivalence relation, provide a clear and concise explanation why not. More specifically, identify a property (reflexive/symmetric/transitive) that it fails to have, and give specific pair(s) that demonstrate the shortcoming. If there are multiple issues, it suffices to identify one of them.

	1. The relation $\{(2, 2), (4, 4), (6, 6), (8, 8), (0, 0), (3, 3), (2, 4), (2, 8), (4, 2), (8, 2), (3, 6), (6, 3)\}$ defined on the set $\{2, 4, 6, 8, 0, 3\}$.
		1. Not an equivalence relation. Not transitive because (4,2) and (2,8) are in the relation but not (4,8)
	2. The relation $\{(m, p) ∈ W × W : 2 ∗ m > p\}$ defined on the set W = $\{1, 2, 3, 4\}$
		2. Not an equivalence relation. Not transitive because (2, 3) and (3, 4) are in the relation but not (2,4)
	3. The relation $\{(c, d) ∈ Z × Z : c^2 = d^2\}$ defined on the set Z
		1. $[x]=\{−x,x\}$ for $x∈Z^+$
		2. $[0] = \{0\}$
	4. The relation $\{(b_{1}, b_{2})$ : the rightmost bit of $b_1$ is the same as the leftmost bit of $b_{2}\}$ defined on the set of bit strings $\{01, 11, 001, 110, 10111, 01000, 1101\}$
		1. Not transitive, (110,001) and (001,11) are in the relation but (110,11) is not
	5. The relation $\{(b_{1}, b_{2})$ : the rightmost bit of $b_{1}$ is the same as the leftmost bit of $b_{2}\}$ defined on the set of bit strings $\{00, 111, 0010, 1101, 00110, 10111\}$
		1. $\{\{00,0010,00110\},\{111,1101,10111\}\}​$


3.  Construct a direct proof of the following claim:
Let A be a set, and let R and S be relations on A. If R and S are both transitive,
then R ∩ S is also transitive.

Proof:(direct)
- Suppose that R and S are both transitive relations on A
- (NTS: $R \cap S$ is transitive)
- Consider an arbitrary elements $a,b,c \in A$ such that
	- $(a,b) \in R \cap S$
	- $(b,c) \in R \cap S$
- By definition of intersection:
	- $(a,b) \in R$, $(a,b) \in S$
	- $(b,c) \in R$, ${b,c} \in S$
- Because R and S are transitive and contain (a,b) and (b,c), they both must contain (a,c)
- Since (a,c) is in R and S, it follows that $(a,c) \in R \cap S$
- Since a,b,c were arbitrary elements, $R \cap S$ is transitive


4. Construct a direct proof of the following claim:
Let A be a set, and let $S ⊆ A × A$ be a relation. If S is both symmetric and
antisymmetric, then $S ⊆ {(a, a) : a ∈ A}$.

Proof:(direct)
- Suppose S is both symmetric and antisymmetric
- (NTS: $S \subseteq (a,a) : a \in A$)
- Consider arbitrary element $(x,y) \in S$
- Since S is symmetric and $(x,y) \in S$, $(y,x) \in S$
- Since S is antisymmetric and $(x,y)$ and $(y,x)$ are in S, $x=y$
- Therefore, any $(x,y) \in S$ satisfies x=y
- Since x and y were arbitrary elements, $S \subseteq (a,a) : a \in A$
