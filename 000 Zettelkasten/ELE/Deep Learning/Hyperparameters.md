202601281011
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Network architecture choices that must be determined before training

### Categories

**A. Data Sets**
- Training set
- Validation set
- Testing set

**B. Training Parameters** (determined through experience/adaptive methods)
1. Initial weight values $w_{ij}$
2. [[Learning Rate]] $\eta$ - doesn't have to be constant
3. [[Momentum]] $\mu$ - doesn't have to be constant

**C. Architecture Hyperparameters**
1. Number of layers
2. Number of nodes at each layer
3. Connectivity pattern:
   - Exhaustive (fully connected)
   - Partially connected
   - Sparsely connected

### Tuning
- Often requires experimentation
- Can use grid search, random search, or Bayesian optimization
- Validation set used to evaluate hyperparameter choices

---
### References
