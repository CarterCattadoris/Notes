202602101501
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

The **Input Embedding Layer** is the first component of a [[Transformer]] that converts raw input tokens (like words) into numerical vector representations.

### Function

- Acts as a lookup table mapping each token to a learned embedding vector
- Captures semantic and syntactic properties of tokens
- Similar tokens will have similar vector representations

### How It Works

1. Each token is associated with a unique index
2. The corresponding vector is retrieved from the **embedding matrix**
3. The embedding matrix parameters are learned during training

### Properties

- Vectors are dense, continuous representations
- Dimensionality is a hyperparameter (e.g., 512, 768)
- Values adjust during training based on the data
