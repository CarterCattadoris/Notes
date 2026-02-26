202602261030
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

**Overfitting** occurs when a neural network learns the training data too well, including its noise, and fails to generalize to unseen data.

### Cause

- More neurons provide greater representation power but increase overfitting risk.
- A network with many parameters can memorize training examples rather than learning underlying patterns.

### Detection

Monitored via training/validation accuracy over epochs:
- **Little overfitting**: validation accuracy closely tracks training accuracy.
- **Strong overfitting**: large gap between training accuracy (high) and validation accuracy (low/plateaued).

### Addressing Overfitting

- [[Regularization]]: adds penalty term $\lambda R(W)$ to the [[Loss Function]] to discourage large weights.
- Increasing $\lambda$ produces simpler (smoother) decision boundaries.
- Proper [[Data Preprocessing]] and [[Weight Initialization]] also help.
- Data split into training, validation, and testing sets allows detection during training.

### Data Split

- **Training set**: used to update weights.
- **Validation set**: used during training to monitor overfitting.
- **Testing set**: used once at the end to evaluate final performance.
