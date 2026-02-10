202602101506
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Self-Attention Mechanism]]

## Content

The **Value Vector** (V) in the [[Self-Attention Mechanism]] stores the actual information that will be used to update the representation of the [[Query Vector|query]].

### Function

- Projection of input data for each sequence element
- Contains the information to be aggregated into the output
- Weighted by [[Attention Score|attention scores]] to determine contribution

### How Values Are Used

1. Attention scores computed from query-key interaction
2. Scores converted to weights via [[Softmax Function]]
3. Value vectors weighted by attention weights
4. Weighted values summed to produce final output

### Example

For translation with values ["chat", "pomme", "arbre", "jus"]:
- Attention weight for "chat" = 0.30
- Attention weight for "pomme" = 0.32 (highest - most relevant)
- Attention weight for "arbre" = 0.15
- Attention weight for "jus" = 0.23

Final output is weighted combination of all value vectors.
