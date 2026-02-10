202602101507
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Self-Attention Mechanism]]

## Content

**Attention Scores** in the [[Self-Attention Mechanism]] indicate how much focus each element in the sequence should receive when processing a particular position.

### Calculation

1. Compute dot product between [[Query Vector]] and all [[Key Vector|Key vectors]]
2. Higher dot products indicate higher relevance
3. Scale by √d_k to prevent extremely large values
4. Apply [[Softmax Function]] to normalize into probability distribution

### Example

For query "apple" with keys ["cat", "apple", "tree", "juice"]:

| Key | Raw Score | After Softmax |
|-----|-----------|---------------|
| cat | 0.9 | 0.30 |
| apple | 0.95 | 0.32 |
| tree | 0.2 | 0.15 |
| juice | 0.6 | 0.23 |

### Purpose

- Determines how much each [[Value Vector]] contributes to output
- Higher scores = more contribution to final representation
- Enables model to "pay attention" to relevant parts of input
