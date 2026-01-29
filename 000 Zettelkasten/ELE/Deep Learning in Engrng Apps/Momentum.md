202601281009
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Term added to [[Gradient Descent]] to help escape local minima

### Update Rule with Momentum
$$\Delta w_i(k+1) = -\eta \frac{\partial e^2}{\partial w_i} + \mu \cdot \Delta w_i(k)$$

Where:
- $\mu$ is the momentum coefficient
- $\Delta w_i(k)$ is the previous weight update

### Purpose
- Helps skip over small error basins (local minima)
- Accelerates convergence in consistent gradient directions
- Dampens oscillations

### Properties
- Does not have to be constant
- Typical values: $0 < \mu < 1$
- Acts like physical momentum - maintains velocity from previous updates

---
### References
