202602261032
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

A **Loss Function** is a generalized performance measure minimized in small steps during training via [[Gradient Descent]].

### General Formula

$$L = \frac{1}{N} \sum_i L_i + \lambda R(W)$$

- **Data loss** $\frac{1}{N} \sum_i L_i$: measures prediction error over $N$ samples.
- **[[Regularization]] loss** $\lambda R(W)$: penalizes model complexity.

### Common Data Loss Types

| Loss | Formula | Use Case |
|------|---------|----------|
| L1 (Least Absolute Deviations) | $\sum |y_i - \hat{y}_i|$ | Robust to outliers |
| L2 ([[Mean Squared Error]]) | $\sum (y_i - \hat{y}_i)^2$ | Regression tasks |
| [[Cross-Entropy Loss]] | $-\sum y_i \log \hat{y}_i$ | Classification tasks |

### Monitoring During Training

- Plot loss vs epoch to diagnose [[Learning Rate]]:
  - **Good rate**: smooth, steady decrease.
  - **Low rate**: very slow decrease.
  - **High rate**: initial plateau then slow decrease.
  - **Very high rate**: loss increases (diverges).
- Noisy loss curves are normal; the overall trend matters.
