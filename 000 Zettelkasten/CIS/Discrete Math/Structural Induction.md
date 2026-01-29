202504081149
Status: #idea
Tags:[[Proofs]]

## Example 1: 
### Claim:
For every full binary tree T, nodes(T) $\geq 2 \cdot height (T) + 1$

### Proof:
By structural induction

Let P(T) be the statement $nodes(T) \geq 2 \cdot height(T) + 1$

### Basis: 
When T is a singleton node, nodes(T) = 1 and height(T) = 0, so $nodes(T) \geq 2 \cdot 0 + 1 = 2 \cdot height (T) + 1$

### Inductive Step:
Suppose $T_{1}$ and $T_{2}$ are full binary trees. For the IH, suppose $P(T_{1}),P(T_{2})$ are true:
$nodes(T_{1}) \geq 2 height(T_{1})+1$ and $nodes(T_{2}) \geq 2height(T_{2})+1$

We NTS $P(T_{1} \bowtie T_{2}$) is true:
$nodes(T_{1} \bowtie T_{2}) \geq 2height(T_{1} \bowtie T_{2}) + 1$

We see that:
$$
nodes(T_{1} \bowtie T_{2}) = 1 + nodes(T_{1} ) + nodes(T_{2})
$$
$$
\geq 1 + 2height(T_{1}) + 1 + 2height(T_{2}) + 1
$$
	^ by IH
$$
= 1 + 2(height(T_{1})+height(T_{2})+1)
$$
	^ by algebra
$$
\geq 1 + 2(max(height(T_{1}),height(T_{2}))+1)
$$
$$
= 1 + 2(height(T_{1} \bowtie T_{2}))
$$
thus, for all $T_{1} \in FBT$ and $T_{2} \in FBt$, 
the conditional $P(T_{1} \land P(T_{2}) \to P(T_{1} \bowtie T_{2})$ is true

by the basis, inductive step, and structural induction, the claim is true

## Example 2

Consider the set $W \subseteq Z \times Z \times Z$ defined recursively
- the tuple (8,1,6) is in W
- the tuple (5,10,4) is in W
- If the tuple (x,y,z) is in W, then the tuple (x+z, y-z, z-3) is in w

### Claim:
For all $(a,b,c) \in W$, a+b is positive and $(a+b) \cdot c \leq 60$

### Proof: 
by structural induction
Let P(a,b,c) be the statement: 
	a+b is positive and $(a+b) \cdot c \leq 60$

### Basis:
P(8,1,6) is true because:
	$8+1 = 9$, which is positive
	$(8+1) \cdot 6 = 54 \leq 60$
P(5,10,4) is true because:
	$5+10 = 15$, which is positive
	$(5+10) \cdot 4 = 60 \leq 60$

### Inductive Step:
Suppose $(x,y,z) \in W$. 
For the IH, suppose $P(x,y,z)$ is true: $x+y$ is positive and $(x+y) \cdot z \leq 60$

We NTS: $P(x+z, y-z, z-3)$ is true: 
	$(x+z) + (y-z)$ is positive
	$((x+z)+(y-z)) \cdot (z-3) \leq 60$

We see that:
	$x+z+y-z = x+y$, which is positive by IH
	$((x+z)+(y-z)) \cdot (z-3) = (x+y) \cdot (z-3) = z(x+y)-3(x+y)$

By the IH, $(x+y) \cdot z \leq 60$, and $3(x+y)$ must be positive, because $x+y$ is
Hence, $z(x+y)-3(x+y) \leq 60$, and hence $P(x+z, y-z, z-3)$ is true

Thus, for all $(x,y,z) \in W$, the conditional:
$P(x,y,z) \to P(x+z, y-z, z-3)$ is true

By the basis, inductive step, and structural induction, the claim is true
