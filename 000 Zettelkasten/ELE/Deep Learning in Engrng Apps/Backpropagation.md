202601281010
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Algorithm for training multi-layer [[Feedforward Neural Network]] using [[Gradient Descent]]

### Network Structure
$$h_j = f(\sum_i x_i w_{ij})$$
$$y = \sum_j w_j f(\sum_i x_i w_{ij})$$

### Weight Update for Hidden Layer
$$\Delta w_{ij} = -\eta \frac{\partial(e^2)}{\partial w_{ij}}$$

Using chain rule:
$$\frac{\partial(e^2)}{\partial w_{ij}} = 2e \cdot w_j \cdot f'(s_j) \cdot x_i$$

Therefore:
$$\Delta w_{ij}^{(k+1)} = -\eta \cdot 2e \cdot w_j \cdot f'(s_j) \cdot x_i$$

### With Momentum
$$\Delta w_{ij}^{(k+1)} = -\eta \cdot 2e \cdot w_j \cdot f'(s_j) \cdot x_i + \mu \cdot \Delta w_{ij}(k)$$

### Key Insight
Error propagates backward from output layer to hidden layers
- Output layer weights updated first
- Hidden layer weights updated using propagated error

---
### References
