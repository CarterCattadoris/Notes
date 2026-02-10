202602101508
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Transformer]]

## Content

**Multi-Head Attention** is the core mechanism of the [[Transformer]] that runs multiple [[Self-Attention Mechanism|self-attention]] operations in parallel, allowing the model to attend to different aspects of the input simultaneously.

### How It Works

1. Input is projected through h different linear layers for Q, K, V
2. [[Self-Attention Mechanism|Scaled dot-product attention]] computed for each "head"
3. Outputs concatenated together
4. Final linear projection produces output

### Advantages

- Captures different types of relationships in parallel
- One head might focus on syntactic relationships
- Another head might focus on semantic relationships
- Allows model to "pay attention" to different parts of input to varying degrees

### Architecture

The multi-head attention layer typically includes:
- Multiple parallel attention heads
- Concatenation of head outputs
- Final linear transformation

### Role in Transformer

- Appears in both encoder and decoder
- Transforms representations from previous layers
- Enables learning complex relationships beyond single attention
