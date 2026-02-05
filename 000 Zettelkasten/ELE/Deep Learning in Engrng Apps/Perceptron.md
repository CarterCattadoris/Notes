202601281012
Status: #idea
Tags: [[Deep Learning (ELE400)]]

The earliest artificial neural network, used for [[Binary Classification]]

### Structure
$$s = \sum_j x_j w_j$$
$$y = h(s) = \begin{cases} +1 & \text{when } s > 0 \\ -1 & \text{when } s \leq 0 \end{cases}$$

- Weighted summation followed by step [[Activation Functions|activation function]]
- Input and weight vectors include a bias term

### Perceptron Learning Algorithm
For iteration $k$, when there's a misclassification:

$$\Delta w_i = \eta \cdot x_i \cdot d$$

Where $d$ is the desired class (+1 or -1)

### Learning Rule Derivation
We want $\Delta s \cdot d > 0$ to move in correct direction
- If $s > 0$ but $d = -1$: need $\Delta s < 0$
- If $s < 0$ but $d = +1$: need $\Delta s > 0$

Setting $\Delta w_i = \eta \cdot x_i \cdot d$ guarantees this since $\sum \Delta w_i \cdot x_i \cdot d = \eta(x_i \cdot d)^2 > 0$

### Limitations
1. Only works for linearly separable data
2. Binary classification only
3. Cannot solve XOR problem

See also: [[Linear Separability]], [[Multi-class Classification]]
sigmoid, ReLU, etc
---
### References
