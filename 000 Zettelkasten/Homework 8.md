I did not receive any assistance on this assignment
## Problem 1:
### Claim:  
For every natural number $m$, $13^m - 4^m$ is divisible by 9.

### Proof: 
by mathematical induction
\### Basis: 
P(1) is true because $13^1-4^1=9$ which is divisible by 9

### Inductive Step:
Suppose $k \geq 1$. For the IH, suppose P(k) is true:
$13^k-4^m$ is divisible by 9

We need to show that P(k+1) is true: $13^{k+1} - 4^{k+1}$ is divisible by 9
By algebra:
$$
13^{k+1} - 4^{k+1} = 13 \cdot 13^k - 4 \cdot 4^k = (9+4) \cdot 13^k - 4 \cdot 4^k = 9 \cdot 13^k + 4(13^k - 4^k)
$$
By the IH, $13^k-4^k$ is divisible by 9, so $4(13^k-4^k)$ is divisible by 9. $9(13^k)$ is divisible by 9 by properties of algebra. Therefore the sum $9 \cdot 13^k + 4(13^k - 4^k)$ is divisible by 9

Thus, for all $k \geq 1$, the conditional $P(k) \to P(k+1)$ is true

By the basis, the inductive step, and the PMI, the claim is true

## Problem 2:

### Claim: 
for every integer $p \geq 1$
$$\sum_{i=1}^{p} \frac{1}{i(i+1)} = 1 - \frac{1}{p+1}$$
### Proof: 
by mathematical induction

Let P(n) be the statement
$$\sum_{i=1}^{n} \frac{1}{i(i+1)} = 1 - \frac{1}{n+1}$$
### Basis:
P(1) is true, because
$$
\frac{1}{1(1+1)} = 1-\frac{1}{1+1} \to \frac{1}{2} = \frac{1}{2}
$$
### Inductive Step:
Suppose $k \geq 1$. For the IH, suppose P(k) is true:
$$\sum_{i=1}^{k} \frac{1}{i(i+1)} = 1 - \frac{1}{k+1}$$
We need to show that P(k+1) is true:
$$\sum_{i=1}^{k+1} \frac{1}{i(i+1)} = 1 - \frac{1}{k+2} = \sum_{i=1}^{k} \frac{1}{i(i+1)} + \frac{1}{(k+1)(k+2)} = \left( 1-\frac{1}{k+1} \right) + \frac{1}{(k+1)(k+2)}$$
$$
=1-\left( \frac{1}{k+1}-\frac{1}{(k+1)(k+2)} \right)=1-\left( \frac{k+2-1}{(k+1)(k+2)} \right)=1-\frac{k+1}{(k+1)(k+2)} = 1-\frac{1}{k+2}
$$
Thus, for all $k \geq 1$, the conditional $P(k) \to P(k+1)$ is true

By the basis, inductive step, and the PMI, the claim is true.

## Problem 3:

### Claim:
Let T be a transitive relation on the set A. For every integer $i ≥ 1, T^i ⊆ T$

### Proof:
by mathematical induction

Let P(n) be the statement $T^n \subseteq T$
### Basis:
P(1) is true, because $T^1 = T$, therefore $T^1 \subseteq T$

### Inductive Step:
Suppose $K \geq 1$. For the IH, suppose P(k) is true:
$$
T^k \subseteq T
$$
We NTS that P(k+1) is true:
$$
T^{k+1} \subseteq T
$$
- Consider arbitrary element $(a,b) \in T^{k+1}$. 
- Because $T^{k+1} = T^k \circ T$, $(a,b) \in T^k \circ T$
- By the definition of composition, there exists $w \in A$ such that $(a,w) \in T$ and $(w,b) \in T^k$ 
- By the IH, $(w,b) \in T$, because $T^k \subseteq T$
- Because T is transitive and (a,w), (w,b) are both in T, $(a,b) \in T$ as well.
- Therefore, for all $k≥1$, the conditional $P(k)→P(k+1)$ is true.
By the basis, inductive step, and the principle of mathematical induction, the claim is true.
