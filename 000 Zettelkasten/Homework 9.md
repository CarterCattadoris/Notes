1. Consider the relation R1 = {(1, 1), (2, 2), (2, 4), (2, 5), (3, 3), (3, 6), (4, 4), (5, 4), (5, 5), (6, 6)}, defined on the set A1 = {1, 2, 3, 4, 5, 6}.  
Minimal = $\{ 1,2,3 \}$
Maximal = $\{ 1,4,6 \}$

2. Consider the relation R2 = {(7, 7), (7, 8), (8, 8), (8, 9), (9, 9), (9, 8), (0, 0)}, defined on the set  A2 = {7, 8, 9, 0}.  
Not a partial order, $(8,9),(9,8) \in R_{2}$ and $8 \neq 9$ so violates antisymmetry

3. Consider the relation R3 = {(1, 1), (2, 2), (3, 2), (3, 3)} ∪ {(x, y) ∈ Z+ × Z+ : x > 3 and x ≤ y},  defined on the set A3 = Z+.  
minimal = {1} and $\{ x \in Z^+ : x \geq 4 \}$

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

5. As discussed in lecture, the set FBT of full binary trees can be defined recursively as follows:  
• A single node is a full binary tree.  
• If T1 and T2 are both full binary trees, then $T1 \bowtie T2$ is a full binary tree.  
Recall: The notation $T1 \bowtie T2$ denotes the tree obtained by creating a new root node, with T1 as its left subtree and T2 as its right subtree.  

The number of edges and of nodes of a binary tree T can be calculated using the functions  edges(T) and nodes(T), defined as follows:  
• If T is a single node, then edges(T)  = 0 and nodes(T) = 1.  
• If T is a tree $T1 \bowtie T2$, then  
$edges(T1 \bowtie T2) = 2 + edges(T1) + edges(T2)$ 
$nodes(T1 \bowtie T2) = 1 + nodes(T1) + nodes(T2)$
Your task: Use structural induction to prove the following claim:  
For every full binary tree T , edges(T) = nodes(T ) − 1.  

## Question 5

Let P(A) be the statement: For every full binary tree A, edges(A) = nodes(A) - 1

### Basis:
Let A be a single node tree: by definition edges(A) = 0 and nodes(A) = 1. $0 = 1-1$ so the base case holds
For the IH, assume 
- $edges(T1 \bowtie T2) = 2 + edges(T1) + edges(T2)$
- 
### IS:
Let $A = A_{1} \bowtie A_{2}$

For the IH, assume the property holds for $A_{1}$ and $A_{2}$:
$edges(A_{1}) = nodes(A_{1})-1$ and $edges(A_{2}) = nodes(A_{2})-1$ 

NTS: $edges(A_{1} \bowtie A_{2}) = nodes(T_{1} \bowtie T_{2}) - 1$

by IH:
$edges(A_{1} \bowtie A_{2}) = 2+(nodes(A_{1})-1)+(nodes(A_{2})-1)=nodes(A_{1})+nodes(A_{2})$
Also by IH:
$nodes(A_{1} \bowtie A_{2})-1=(1+nodes(A_{1})+nodes(A_{2}))-1=nodes(A_{1})+nodes(A_{2})$