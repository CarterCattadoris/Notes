202504081149
Status: #idea
Tags:[[Proofs]]

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
nodes(T_{1} \bowtie T_{2}) = 1 +
$$