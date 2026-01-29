202601281007
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Optimization algorithm that minimizes error by moving weights in the direction of steepest descent

### Update Rule
$$\Delta w_i = -\eta \frac{\partial(e^2)}{\partial w_i}$$

Where:
- $\eta$ is the [[Learning Rate]]
- $\frac{\partial(e^2)}{\partial w_i}$ is the partial derivative of squared error with respect to weight $w_i$

### Intuition
- If slope is positive, decrease weight
- If slope is negative, increase weight
- Move toward the minimum of the error surface

### For Linear Neuron
$$\frac{\partial(e^2)}{\partial w_1} = 2e \cdot x_1$$
$$\Delta w_1 = -\eta \cdot 2e \cdot x_1$$

### Local Minima Problem
Error surface may have multiple local minima
- Algorithm can get stuck in local minimum
- Solution: Add [[Momentum]] term

$$\Delta w_i(k+1) = -\eta \frac{\partial e^2}{\partial w_i} + \mu \cdot \Delta w_i(k)$$

---
### References
