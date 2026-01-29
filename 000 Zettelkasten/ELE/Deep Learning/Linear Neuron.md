202601281001
Status: #idea
Tags: [[Deep Learning (ELE400)]]

A single computational unit that performs weighted summation of inputs

$$y = \sum_{i} x_i w_i = x_1 w_1 + x_2 w_2 + ... + x_n w_n$$

- Equivalent to linear regression: $y = mx + b$
- $x_i$ are inputs, $w_i$ are weights
- Can include a bias term by setting $x_n = 1$ and $w_n = b$

### Limitation
If all neurons are linear, a neural network collapses to a single neuron
- Multiple layers of linear neurons = equivalent to one linear neuron
- This is why we need [[Nonlinear Neuron]] for deeper networks

### Applications
1. Function approximation (linear)
2. [[Linear Regression]]

[[Mean Squared Error]] is used to measure error during training

---
### References
