202601281023
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Network for [[Unsupervised Learning]] where neurons compete to respond to inputs

### Structure
- Same topology as [[Hamming Network]]
- Competitive output layer (winner=1, rest=0)
- Real-valued inputs and weights $\in [-1, +1]$
- Learning utilizes Euclidean distances and weight, not [[Hamming Distance]]

### Learning Rule
For winning node $j^*$ (closest to input pattern $k$):

$$\Delta w_{j^*,l} = \eta(i_{k,l} - w_{j^*,l}) \quad \text{for } l \in \{1, 2, ..., n\}$$

Where:
- $w_{j,l}$: connection weights for output node $j$
- $i_{k,l}$: $k$-th input pattern
- $\eta$: [[Learning Rate]]

### Finding Closest Node
For real-valued vectors, use Euclidean distance:
$$d_j = \sqrt{\sum_l (i_{k,l} - w_{j,l})^2}$$

Smallest $d_j$ determines winner $j^*$

### Weight Update Effect
Moves winning node's weight vector toward the input pattern

---
### References
