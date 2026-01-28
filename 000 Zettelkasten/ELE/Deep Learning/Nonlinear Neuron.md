202601281002
Status: #idea
Tags: [[Deep Learning (ELE400)]]

A neuron that applies a nonlinear [[Activation Functions|activation function]] to the weighted sum

$$s = \sum_{i} x_i w_i$$
$$y = f(s)$$

Where $f(s)$ is a nonlinear function

### Why Nonlinearity?
- Linear networks collapse to a single neuron regardless of depth
- Nonlinearity allows networks to approximate any continuous function
- Enables learning of complex, nonlinear relationships

### Common Activation Functions
See [[Activation Functions]] for details:
- Step Function
- Sigmoid: $y = \frac{1}{1 + e^{-k \cdot s}}$
- ReLU (Ramp)
- Gaussian

### Network Output
For a hidden layer: $h_j = f(\sum_i x_i w_{ij})$
For output: $y = \sum_j h_j w_j$

---
### References
