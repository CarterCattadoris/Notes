202602101509
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

The **Softmax Function** converts a vector of real numbers into a probability distribution where all values sum to one.

### Formula

$$\sigma(z)_i = \frac{e^{z_i}}{\sum_j e^{z_j}}$$

### Properties

- Output values are in range (0, 1)
- All outputs sum to exactly 1
- Larger inputs produce larger outputs (preserves ordering)
- Acts like a "soft" version of argmax

### Use in Transformers

In [[Self-Attention Mechanism]]:
1. [[Attention Score|Attention scores]] passed through softmax
2. Creates probability distribution over sequence positions
3. Determines attention weights for [[Value Vector|value vectors]]
4. Higher scores receive higher weights

### Use in Output Layer

- Final layer of [[Transformer]] uses softmax
- Produces probability distribution over vocabulary
- Highest probability token selected as output
