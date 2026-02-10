202602101511
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

A **Residual Connection** (or skip connection) is a shortcut that allows the gradient to flow directly from the output of a layer to its input, bypassing the layer's transformation.

### Formula

$$\text{output} = \text{LayerOutput}(x) + x$$

The input x is added directly to the layer's output.

### Purpose

- Mitigates the **vanishing gradient problem** in deep networks
- Allows training of much deeper networks
- Enables gradient to flow directly through skip connection
- Helps preserve information from earlier layers

### In Transformers

- Used after [[Multi-Head Attention]] layers
- Used after [[Feedforward Neural Network]] layers
- Combined with [[Layer Normalization]] ("Add & Norm" blocks)

### Benefits

- Easier optimization of deep networks
- Better gradient flow during [[Backpropagation]]
- Allows network to learn identity mapping if needed
