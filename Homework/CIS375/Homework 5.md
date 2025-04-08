I did not receive assistance on this assignment
## Question 1
Consider the following relations defined on the set {a, b, c, d}:  
$T_{1} = \{(a, a), (a, b), (c, b), (d, a), (d, b)\}$
$T_{2} = \{(a, b), (a, c), (b, d), (c, a), (d, c)\}$
$(T_{1} \cap T_{2}) = \{ (a,b)\}$
Calculate the following:  
a. $T_{2}^{−1} = \{ (b,a),(c,a),(d,b),(a,c),(c,d) \}$
b. $(T1 ∩ T2)^{−1} = \{(b,a)\}$ 
c. $T1 ◦ T2 = \{ (a,b),(b,a),(b,b),(c,a),(c,b),(d,b) \}$
d. $id_{\{a,b,c,d\}} = \{(a,a),(b,b),(c,c),(d,d)\}$


## Question 2
Consider the following relations defined on the set {a, b, c, d}:  
$S_{1} = \{(a, a), (a, b), (b, b), (c, b), (c, c), (d, b)\}$
$S_{2} = \{(a, a), (a, b), (a, c), (b, a), (c, a)\}$
$S_{3} = \{(a, d), (a, b), (c, b), (c, d)\}$
$S_{4} = \{(a, b), (c, b), (b, c), (b, a), (d, c), (a, a), (b, b), (c, c), (d, d)\}$

a. Which of these four relations is not reflexive? For each one, provide a brief counterexample to support your answer. 
$S_{1}$ is not reflexive because it is missing (d,d)
$S_{2}$ is not reflexive because it is missing (b,b)
$S_{3}$ is not reflexive because $S_{3}$ does not contain (a,a)

b. Which of these four relations is not irreflexive? For each one, provide a brief counterexample to support your answer.  
$S_{1}$ is not irreflexive because $S_{1}$ contains (a,a)
$S_{2}$ is not irreflexive because it has (a,a)
$S_{4}$ is not irreflexive because it has (a,a)

c. Which of these four relations is not symmetric? For each one, provide a brief counterexample to support your answer.  
$S_{1}$ is not symmetric because $(a,b) \in S_{1}$ but $(b,a) \not\in S_{1}$ 
$S_{3}$ is not symmetric because $(a,b) \in S_{3}$ but $(b,a) \not\in S_{3}$ 
$S_{4}$ is not symmetric because $(d,c) \in S_{4}$ but $(c,d) \not\in S_{4}$ 

d. Which of these four relations is not antisymmetric? For each one, provide a brief counterexample to support your answer.  
$S_{2}$ is not antisymmetric because $(a,b) \in S_{2}$ and $(b,a) \in S_{2}$ and $b \neq a$
$S_{4}$ is not antisymmetric because $(c,b) \in S_{4}$ and $(b,c) \in S_{4}$ and $b \neq c$

e. Which of these four relations is not transitive? For each one, provide a brief counterexample to support your answer
$S_{2}$ is not transitive because $(b,a) \in S_{2}$ and $(a,b) \in S_{2}$ but $(b,b) \not\in S_{2}$
$S_{4}$ is not transitive because $(a,b) \in S_{4}$ and $(b,c) \in S_{4}$ but $(a,c) \not\in S_{4}$

## Question 3
For each of the following relations, determine whether or not it is reflexive, irreflexive,  symmetric, antisymmetric, and/or transitive.  
For each property, support your answer with either a proof sketch (if the property holds) or a  counterexample (if the property does not hold). 

1. $R_{1} = \{(x, y) ∈ N × N : x + y$ is even} as a relation on N  
	1. Reflexive: Yes. Consider any $n \in N: (n,n) \in R_{1}$ because $n+n=2n$ which is even
	2. Irreflexive: No. $(17,17) \in R_{1}$ because $17+17=34$ which is even
	3. Symmetric: Yes. Consider any $x,y \in N$ such that $(x,y)\in R_{1}$ then x+y is even and so is y+x, so $(y,x)\in R_{1}$
	4. Anti Symmetric: No. (1,3) and (3,1) are in $R_{1}$ since $1+3=3+1=4$, but $1 \neq 3$
	5. Transitive: Yes. Consider any x,y,z such that $(x,y) \in R_{1}$ and $(y,z) \in R_{1}$, which means x+y is even and y+z is even. $x+z = (x+y)+(y+z) - 2y$, which must be even so $(x,z) \in R_{1}$

2. $R_{2} = {(x, y) ∈ N × N : x + y = 0}$ as a relation on N  
	6. Reflexive: No, $x+y=0$ is not true for all $x,y \in N \times N$
	7. Irreflexive: No. $(0,0) \in R_{2}$ because 0+0=0
	8. Symmetric: Yes. Since $(0,0)$ is the only element of $R_{2}$, it must be symmetric
	9. Anti Symmetric:Yes. Since  $(0,0)$ is the only element of $R_{2}$ and 0=0, it must be antisymmetric
	10. Transitive: Yes. if $(x,y) = (0,0)$, $(y,z)=(0,0)$, $(x,z)=(0,0)$
3. $R_{3} = {(x, y) ∈ Z × Z : x = y + 1}$ as a relation on Z
	1. Reflexive: No. we would need x=x+1 to satisfy the form $(x,x) \in R_{3}$, which is impossible
	2. Irreflexive:Yes. Since it is impossible to satisfy reflexivity it is irreflexive
	3. Symmetric:No. For $R_{3}$ to be symmetric we would need $x=y+1$ and $y=x+1$, which implies y=y+2 which is false
	4. Anti Symmetric:Yes. Since it is not possible for $R_{3}$ to be symmetric anywhere, it is antisymmetric
	5. Transitive: No. We would need to satisfy $x = y+1$, $y = z+1$ and $x=z+1$. When you combine these statements you get $x=z+2$ which is impossible by the definition