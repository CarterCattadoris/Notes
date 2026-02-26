202602261034
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

**Weight Initialization** determines the starting values of weights before training a neural network. The choice significantly affects learning speed and convergence.

### Strategy 1: Initialize to Zeros

All weights $w_i(0) = 0$.

**Problem**: every iteration follows the same path. Since $\sum w_i x_i = 0$ for all neurons, all neurons compute the same output and receive the same gradient update. The network cannot break symmetry and effectively behaves as a single neuron.

### Strategy 2: Random from $N(0, 1)$

Sample weights from a standard normal distribution.

**Problem**: with a large number of neurons $n$, the weighted sum $\sum w_i x_i$ can become very large in magnitude. For sigmoid/tanh [[Activation Functions]], this pushes outputs into the flat (saturated) region where $f'(s) \approx 0$, causing vanishing gradients and slowing learning.

### Strategy 3: Random from $N(0, 1) \cdot \sqrt{1/n}$

Scale random weights by $\sqrt{1/n}$, where $n$ is the number of inputs to the neuron.

**Advantage**: addresses both drawbacks above. The variance of the weighted sum stays controlled regardless of $n$, keeping activations in the useful range of the [[Activation Functions|activation function]].

This is known as **Xavier/Glorot initialization** (for sigmoid/tanh) from the paper "Understanding the difficulty of training deep feedforward neural networks."
