202601281008
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Parameter $\eta$ that controls the step size in [[Gradient Descent]]

$$\Delta w_i = -\eta \frac{\partial(e^2)}{\partial w_i}$$

### Constraints
$$0 < \eta << 1$$

### Effects
- **Too large**: Overshoots minimum, may oscillate or diverge
- **Too small**: Very slow convergence
- **Just right**: Smooth convergence to minimum

### Adaptive Learning Rate
- Does not have to be constant
- Can decrease over time (learning rate scheduling)
- Adaptive methods adjust per-parameter (Adam, RMSprop)

---
### References
