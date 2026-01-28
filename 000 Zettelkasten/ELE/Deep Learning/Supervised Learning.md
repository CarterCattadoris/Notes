202601281006
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Learning paradigm where the network is trained using labeled input-output pairs

### Training Data Format
$(x_1, x_2, ..., x_n, d)$ where $d$ is the desired output

### Process
1. Present input to network
2. Compute output $y$
3. Calculate error: $e = y - d$
4. Update weights to reduce error using [[Gradient Descent]]

### For Linear Neuron
$$y = x_1 w_1 + x_2 w_2 + w_3$$
$$e^2 = (x_1 w_1 + x_2 w_2 + w_3 - d)^2$$

Weight update: $\Delta w_i = -\eta \cdot 2e \cdot x_i$

### For Nonlinear Neuron
$$y = f(x_1 w_1 + x_2 w_2 + w_3)$$
Weight update: $\Delta w_i = -\eta \cdot 2e \cdot f'(s) \cdot x_i$

Requires derivative of [[Activation Functions]]

### Key Parameters
- [[Learning Rate]] ($\eta$)
- [[Momentum]] ($\mu$)
- Initial weight values

See also: [[Backpropagation]], [[Unsupervised Learning]]

---
### References
