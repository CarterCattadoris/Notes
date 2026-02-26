202602261031
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

**Regularization** is a technique that adds a penalty term to the [[Loss Function]] to prevent [[Overfitting]] by discouraging large weights.

### General Form

The regularization term $\lambda R(W)$ is added to the data loss:

$$L = \underbrace{\frac{1}{N} \sum_i L_i}_{\text{data loss}} + \underbrace{\lambda R(W)}_{\text{regularization loss}}$$

Where $\lambda$ is the **regularization strength** [[Hyperparameters|hyperparameter]].

### L2 Regularization

For every weight $w$ in the network, the term $\frac{\lambda w^2}{2}$ is added to the objective.

$$R(W) = \sum_k \sum_l W_{k,l}^2$$

- Penalizes large weights quadratically.
- Encourages small, distributed weights.

### L1 Regularization

For every weight $w$ in the network, the term $\lambda |w|$ is added to the objective.

$$R(W) = \sum_k \sum_l |W_{k,l}|$$

- Encourages sparsity (many weights become exactly zero).
- Produces simpler models.

### Effect of $\lambda$

- Small $\lambda$ (e.g., 0.001): complex decision boundaries, higher overfitting risk.
- Large $\lambda$ (e.g., 0.1): smoother decision boundaries, less overfitting but potentially underfitting.
