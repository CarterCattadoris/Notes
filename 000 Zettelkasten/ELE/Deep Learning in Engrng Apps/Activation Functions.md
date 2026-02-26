202601281003
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

Nonlinear functions applied to the weighted sum $s = \sum_i x_i w_i$ in a [[Nonlinear Neuron]]. The choice of activation function directly impacts learning because its derivative $f'(s)$ appears in the weight update rule used by [[Backpropagation]]:

$$\Delta w_{ij} = -\eta \cdot 2e \cdot w_j \cdot f'(s_j) \cdot x_i$$

If $f'(s) = 0$, the weights stop updating entirely.

---

### Step Function
$$y = \begin{cases} +1 & \text{when } s > 0 \\ -1 & \text{when } s \leq 0 \end{cases}$$
- Used in [[Perceptron]] for [[Binary Classification]]

**Advantages:**
- Simple to compute
- Clear binary decision boundary

**Disadvantages:**
- Not differentiable at $s = 0$, so gradient-based learning (e.g., [[Backpropagation]]) cannot be applied
- No gradient information means weights cannot be updated incrementally
- Outputs only two values, no notion of confidence

---

### Sigmoid Function
$$y = \frac{1}{1 + e^{-k(s)}}$$
- Output range: $(0, 1)$
- Smooth, differentiable everywhere
- Derivative: $f'(s) = f(s)(1 - f(s))$, easy to compute from the output itself

**Advantages:**
- Continuous and differentiable, enabling [[Backpropagation]]
- Output interpretable as a probability
- Smooth gradient provides stable learning

**Disadvantages:**
- Vanishing gradient: for large $|s|$, $f'(s) \approx 0$, causing weight updates to stall in deep networks
- Output is not zero-centered (always positive), which can slow convergence during training
- Exponential computation is more expensive than simpler functions

---

### Tanh (Hyperbolic Tangent)
$$y = \tanh(s) = \frac{e^s - e^{-s}}{e^s + e^{-s}}$$
- Output range: $(-1, 1)$
- Related to sigmoid: $\tanh(s) = 2\sigma(2s) - 1$
- Derivative: $f'(s) = 1 - \tanh^2(s)$

**Advantages:**
- Zero-centered output, so positive and negative values flow naturally through the network
- Stronger gradients than sigmoid near $s = 0$ (derivative peaks at 1 vs. 0.25 for sigmoid)
- Still smooth and differentiable everywhere

**Disadvantages:**
- Still suffers from vanishing gradient for large $|s|$
- Exponential computation cost, similar to sigmoid
- Saturates at both extremes just like sigmoid

---

### Ramp (Piecewise Linear / ReLU)
$$y = \max(0, s)$$
- Linear in active region ($s > 0$), zero below threshold

**Advantages:**
- Computationally efficient: no exponential calculations
- Does not saturate for positive inputs, reducing the vanishing gradient problem
- Produces sparse activations (many neurons output zero), which can improve efficiency

**Disadvantages:**
- Dying ReLU problem: neurons with $s < 0$ have $f'(s) = 0$, so those weights never update
- Not differentiable at $s = 0$ (in practice, a subgradient is used)
- Output is not zero-centered (always $\geq 0$)

---

### Gaussian / Raised Cosine
- Bell-shaped response centered around $s = 0$
- Used in radial basis function networks

**Advantages:**
- Localized activation: responds strongly only near a specific input region
- Useful for problems requiring local feature detection

**Disadvantages:**
- Not monotonic, which can complicate optimization
- Gradient vanishes for both large positive and large negative $s$
- Less commonly used in deep networks due to training difficulty

---
### References
