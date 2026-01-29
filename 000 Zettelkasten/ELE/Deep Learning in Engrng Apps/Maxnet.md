202601281022
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Recurrent network that finds the node with maximum value - used with [[Hamming Network]]

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

---
### References
