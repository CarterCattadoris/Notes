202602101504
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Self-Attention Mechanism]]

## Content

The **Query Vector** (Q) in the [[Self-Attention Mechanism]] represents the element of interest or the context that you want to obtain information about.

### Function

- Derived from the current position in the input sequence
- Used to determine similarity/relevance between this context and other elements
- Compared against [[Key Vector|Key vectors]] to compute attention

### Example: Translation Task

Translating English to French, at the word "apple":
- **Query**: "apple" (the word you want to translate)
- **Keys**: ["cat", "apple", "tree", "juice"] (all English words)
- **Values**: ["chat", "pomme", "arbre", "jus"] (French translations)

The query is used to find which keys (and their corresponding values) are most relevant.

### Properties

- Learned projection of input embeddings
- Dimension matches key vector dimension for dot product compatibility
