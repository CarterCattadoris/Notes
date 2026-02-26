202601281004
Status: #idea
Tags: [[Deep Learning (ELE400)]]

A neural network where information flows in one direction: input to output

### Structure
- **Input Layer**: Receives input data
- **Hidden Layer(s)**: Intermediate processing
- **Output Layer**: Produces final result

### Types
- [[Linear Feedforward Neural Network]] - all neurons linear
- [[Nonlinear Feedforward Neural Network]] - contains nonlinear activation

### Key Property
For function approximation:
- Only 1 hidden layer is theoretically needed (Universal Approximation Theorem): a network with at least one hidden layer with a nonlinear [[Activation Functions|activation function]] can approximate any function with arbitrarily large number of neurons ("universal approximators").
- Theoretically, deep and shallow networks have equal representational power.
- Empirically, deeper networks (multiple hidden layers) work better than single-hidden-layer networks.
- More hidden neurons = greater representation power but higher [[Overfitting]] risk. Use [[Regularization]] to control this.
- "Deep" networks have many hidden layers (e.g., GPT-3 has 96 layers).

### Training Considerations
- Proper [[Weight Initialization]] is critical for deep networks.
- [[Data Preprocessing]] (mean subtraction, normalization) improves convergence.
- Monitor [[Loss Function]] vs epoch, training/validation accuracy, and weight update ratios (~1e-3) during training.

### GPT-3 Parameters
- Layers: 96
- Hidden Nodes: >12,000
- Parameters: 175 billion
- Sequence length: 2048

---
### References
