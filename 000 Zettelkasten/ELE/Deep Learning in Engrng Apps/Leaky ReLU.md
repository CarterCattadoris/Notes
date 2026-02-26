202602261035
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

**Leaky ReLU** is a variant of the ReLU [[Activation Functions|activation function]] that allows a small gradient for negative inputs, addressing the dying ReLU problem.

### Formula

$$y = \begin{cases} x & \text{for } x \geq 0 \\ \alpha x & \text{for } x < 0 \end{cases}$$

Where $\alpha$ is a small constant (e.g., 0.01).

### Comparison with ReLU

| Property | ReLU | Leaky ReLU |
|----------|------|------------|
| Positive region | $y = x$ | $y = x$ |
| Negative region | $y = 0$ | $y = \alpha x$ |
| Gradient for $x < 0$ | 0 (dead) | $\alpha$ (small but nonzero) |
| Dying neuron problem | Yes | No |

### Advantage

- Neurons with negative inputs still receive gradient updates, preventing them from permanently dying.
- Retains all benefits of ReLU: computationally efficient, no saturation for positive inputs.
