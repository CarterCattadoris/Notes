202602101502
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

**Positional Encoding** is a mechanism that adds information about the position of each token within a sequence to the [[Input Embedding Layer|input embedding]].

### Why It's Needed

- [[Transformer|Transformers]] process inputs in parallel, losing inherent positional information
- Word order matters significantly in tasks like natural language processing
- Without positional encoding, "dog bites man" and "man bites dog" would be indistinguishable

### Why Not Use Indices?

- For long sequences, index values grow large in magnitude.
- Normalizing indices to [0,1] creates problems for variable-length sequences (different sequences normalized differently).
- Instead, transformers use a scheme based on **sine and cosine functions of varying frequencies**.

### Sinusoidal Formulas

For token at position $k$ and embedding dimension index $i$:

$$P(k, 2i) = \sin\left(\frac{k}{n^{2i/d}}\right)$$
$$P(k, 2i+1) = \cos\left(\frac{k}{n^{2i/d}}\right)$$

- $d$: dimension of the output embedding space.
- $n$: user-defined scalar (e.g., 10,000).
- Even indices use sine, odd indices use cosine.

### Example: "I am a robot" (d=4, n=100)

| Token | k | P(k,0) sin | P(k,1) cos | P(k,2) sin | P(k,3) cos |
|-------|---|------------|------------|------------|------------|
| I | 0 | 0 | 1 | 0 | 1 |
| am | 1 | 0.84 | 0.54 | 0.10 | 1.0 |
| a | 2 | 0.91 | -0.42 | 0.20 | 0.98 |
| Robot | 3 | 0.14 | -0.99 | 0.30 | 0.96 |

### Properties

- Each position gets a **unique** encoding vector.
- Added directly to the input embeddings (element-wise addition).
- Can be learned or fixed (original paper used fixed sinusoidal).
