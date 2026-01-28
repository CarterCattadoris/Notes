202601281014
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Property where two classes can be separated by a single hyperplane

### Linearly Separable
- AND gate: separable
- OR gate: separable
- Single [[Perceptron]] can learn these

### Not Linearly Separable
- XOR gate: NOT separable
- Requires multiple decision boundaries
- Need multi-layer network to solve

### XOR Problem
| A | B | XOR |
|---|---|-----|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

No single line can separate 0s from 1s

### Solution
Use [[Nonlinear Feedforward Neural Network]] with hidden layers

---
### References
