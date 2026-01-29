202601281742
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Supervised learning method for predicting continuous outputs using linear relationships

### Model
$$y = w_0 + w_1 x_1 + w_2 x_2 + ... + w_n x_n = \mathbf{w}^T \mathbf{x}$$

### Training Objective
Minimize [[Mean Squared Error]] between predictions and targets:
$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

### Solution Methods
1. Closed-form (Normal equation): $\mathbf{w} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$
2. [[Gradient Descent]] - iterative optimization

### Connection to Neural Networks
- [[Linear Neuron]] performs linear regression
- Single layer [[Linear Feedforward Neural Network]]

---
### References
