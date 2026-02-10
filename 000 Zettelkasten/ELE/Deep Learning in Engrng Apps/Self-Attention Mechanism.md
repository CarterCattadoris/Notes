202602101503
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

The **Self-Attention Mechanism** (also called **Scaled Dot-Product Attention**) analyzes different parts of an input sequence simultaneously to determine which parts are most important for each position.

### Components

1. **[[Query Vector]]** - Represents the current focus/element of interest
2. **[[Key Vector]]** - Represents elements being compared to the query
3. **[[Value Vector]]** - Stores the actual information to be aggregated

### Process

1. Compute Q, K, V vectors for each token (learned during training)
2. Calculate [[Attention Score|attention scores]] via dot product of Q and K
3. Scale scores by √d_k to prevent large values
4. Apply [[Softmax Function]] to get probability distribution
5. Compute weighted sum of V vectors using attention weights

### Attention Formula

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

Where $d_k$ is the dimension of the key vectors.
