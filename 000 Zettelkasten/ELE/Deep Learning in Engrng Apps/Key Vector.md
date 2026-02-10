202602101505
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Self-Attention Mechanism]]

## Content

The **Key Vector** (K) in the [[Self-Attention Mechanism]] is associated with each element in the input sequence and is used to compute relevance to the [[Query Vector]].

### Function

- Projection of input data for each sequence element
- Used to compute how relevant each element is to the query
- Relevance calculated via dot product with query vectors

### Relevance Calculation

The dot product between query and key determines similarity:
- **Higher dot product** = Higher relevance
- **Lower dot product** = Lower relevance

### Example

For query "apple" with keys ["cat", "apple", "tree", "juice"]:
- Dot product(query, "cat") = 0.9 (high similarity)
- Dot product(query, "apple") = 0.95 (very high similarity)
- Dot product(query, "tree") = 0.2 (low similarity)
- Dot product(query, "juice") = 0.6 (moderate similarity)
