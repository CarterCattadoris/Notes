**I did not receive any assistance on this assignment

1. Consider the relation R1 = {(1, 1), (2, 2), (2, 4), (2, 5), (3, 3), (3, 6), (4, 4), (5, 4), (5, 5), (6, 6)}, defined on the set A1 = {1, 2, 3, 4, 5, 6}.  
- Minimal = $\{ 1,2,3 \}$
- Maximal = $\{ 1,4,6 \}$

2. Consider the relation R2 = {(7, 7), (7, 8), (8, 8), (8, 9), (9, 9), (9, 8), (0, 0)}, defined on the set  A2 = {7, 8, 9, 0}.  
- Not a partial order, $(8,9),(9,8) \in R_{2}$ and $8 \neq 9$ so violates antisymmetry

1. Consider the relation R3 = {(1, 1), (2, 2), (3, 2), (3, 3)} ∪ {(x, y) ∈ Z+ × Z+ : x > 3 and x ≤ y},  defined on the set A3 = Z+.  
- minimal = $\{1\}$ and $\{ x \in Z^+ : x \geq 4 \}$
- maximal: $\{ 2 \}$
## Question 4

Let P(s) be the statement $numA(s) > numB(s)$
### Basis:
P(ca) is true because $numA(ca) = 1 > 0 = numB(ca)$
P(acab) is true because $numA(acab) = 2 > 1 = numB(acab)$

### IS:
Suppose s and t are in ABCs
Suppose P(s) and P(t) are true: $numA(s) > numB(s)$, $numA(t) > numB(t)$

We NTS that $P(bsbta)$ is true: $numA(bsbta) > numB(bsbta)$

  $numA(bsbta) = 1 + numA(s) + numA(T)$ def numA
		    $> 1+numB(s) + numA(t)$ by IH
		    $\geq 1+numB(s) + (numB(t) + 1)$ by IH with integer facts
		    $= 2+numB(s) + numB(t) = numB(bsbta)$

Thus, the conditional $P(s) \land P(t) \to P(bsbta)$ is true
By the basis, IS, and structural induction, the claim is true

## Question 5

Let P(A) be the statement: For every full binary tree A, edges(A) = nodes(A) - 1

### Basis:
Let A be a single node tree: by definition edges(A) = 0 and nodes(A) = 1. $0 = 1-1$ so the base case holds

### IS:
Suppose $A_{1}$ and $A_{2}$ are FBTs
Suppose $P(A_{1})$ and $P(A_{2})$ are true:
- $edges(A_{1}) = nodes(A_{1})-1$ 
- $edges(A_{2}) = nodes(A_{2})-1$ 

NTS: $edges(A_{1} \bowtie A_{2}) = nodes(A_{1} \bowtie A_{2}) - 1$

by definition of edges:
$edges(A_{1} \bowtie A_{2}) = 2 + edges(A_{1})+edges(A_{2})$
$= 2+(nodes(A_{1})-1)+(nodes(A_{2})-1)$ -> by IH
$=nodes(A_{1})+nodes(A_{2})$

by definition of nodes:
$nodes(A_{1} \bowtie A_{2})-1=(1+nodes(A_{1})+nodes(A_{2}))-1)$
$=nodes(A_{1})+nodes(A_{2})$

It follows that $edges(A_{1} \bowtie A_{2}) = nodes(A_{1} \bowtie A_{2})-1$

Thus the conditional $P(A_{1}) \land P(A_{2}) \to P(A_{1} \bowtie A_{2})$ is true
By the basis, IS and structural induction the claim is true