202602101502
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

**Positional Encoding** is a mechanism that adds information about the position of each token within a sequence to the [[Input Embedding Layer|input embedding]].

### Why It's Needed

- [[Transformer|Transformers]] process inputs in parallel, losing inherent positional information
- Word order matters significantly in tasks like natural language processing
- Without positional encoding, "dog bites man" and "man bites dog" would be indistinguishable

### Implementation

- Typically calculated using **sinusoidal functions**
- Different frequencies are used for different dimensions of the embedding vector
- Added directly to the input embeddings (element-wise addition)

### Properties

- Allows the model to represent relative positions effectively
- Enables the model to understand token order
- Can be learned or fixed (original paper used fixed sinusoidal)
