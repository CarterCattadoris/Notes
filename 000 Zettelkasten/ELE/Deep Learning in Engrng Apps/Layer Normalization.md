202602101510
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

**Layer Normalization** is a technique that standardizes the inputs to each layer of the model, reducing the chance of being affected by extreme values or unstable gradients.

### Purpose

- Stabilizes training of deep networks
- Reduces internal covariate shift
- Prevents extreme activation values
- Helps with gradient flow

### In Transformers

- Applied after [[Multi-Head Attention]] layers
- Applied after [[Feedforward Neural Network]] layers
- Often combined with [[Residual Connection|residual connections]] ("Add & Norm")

### Difference from Batch Normalization

- Layer norm normalizes across features for each sample
- Batch norm normalizes across batch for each feature
- Layer norm works better for sequence models with variable lengths
