202601281003
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Nonlinear functions applied to the weighted sum in a [[Nonlinear Neuron]]

### Step Function
$$y = \begin{cases} +1 & \text{when } s > 0 \\ -1 & \text{when } s \leq 0 \end{cases}$$
- Used in [[Perceptron]]
- Binary output

### Sigmoid Function
$$y = \frac{1}{1 + e^{-k(s)}}$$
- Output range: $(0, 1)$
- Smooth, differentiable
- Useful for [[Backpropagation]] because derivative is easy to compute

### Ramp (Piecewise Linear / ReLU)
- Linear in active region
- Zero below threshold
- Computationally efficient

### Gaussian / Raised Cosine
- Bell-shaped response
- Used in radial basis function networks

---
### References
