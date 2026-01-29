202601281022
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Recurrent network that finds the node with maximum value - used with [[Hamming Network]]

![[Pasted image 20260129143416.png]]
### Structure
- Single layer with recurrent connections
- Each node has positive self-feedback ($+\theta$)
- Negative connections to all other nodes ($-\epsilon$)

### Parameters
- $\theta = 1$ (self-feedback weight)
- $\epsilon = \frac{1}{\text{number of nodes}}$

### Update Rule
$$\text{sum}_j = \sum_k w_k x_k(t)$$
$$x_j(t+1) = f(\text{sum}_j) = \max(0, \text{sum}_j)$$

All nodes updated simultaneously

### Convergence
- Winner's value stays positive
- All other nodes → 0
- Final state: one node active, rest inactive

### Example
5 nodes with initial values $(0.5, 0.9, 1, 0.9, 0.9)$, $\theta=1$, $\epsilon=0.2$
Node 3 (value 1) will eventually win as the maximum

$x_{k}(t+1) = max\left\{  0, -\sum \epsilon \cdot x_{i} + \Theta x_{k}(t) \right\}$ 

$x_{a} = 1$
$x_{a}(2) = max\left\{  0, -\frac{1}{5}(0.9+0.9+0.9+0.5) + 1 \cdot 1  \right\}$ 
$= max \left\{   0, -\frac{3.2}{5} + 1  \right\}$
$= max\{ 0, 1-0.64 \} = 0.36$

$x_{d} = 0.5$
$x_{d}(2) = max\left\{  0, -\frac{1}{5}(0.9+0.9+0.9+1) + 1 \cdot 0.5  \right\}$
$= max \left\{   0, -\frac{3.7}{5} + 0.5  \right\}$
$= max \{ 0, -0.7+0.5 \} = 0$


---
### References
