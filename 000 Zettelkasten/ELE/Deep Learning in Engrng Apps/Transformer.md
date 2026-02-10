202602101500
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

A **Transformer** is a neural network architecture that processes sequences by transforming an input sequence into an output sequence. Unlike traditional [[Recurrent Neural Network|RNNs]] that process sequences step-by-step, Transformers process entire sequences in parallel.

### Key Components

1. **[[Input Embedding Layer]]** - Converts tokens to vector representations
2. **[[Positional Encoding]]** - Injects position information
3. **[[Multi-Head Attention]]** - Core attention mechanism (repeated N times)
4. **[[Feedforward Neural Network]]** - Applied independently to each position
5. **[[Layer Normalization]]** and [[Residual Connection|Residual Connections]] - Stabilize training
6. **Output Layer** - Linear transformation followed by [[Softmax Function]]

### Advantages Over Traditional Approaches

- Processes long sequences with **parallel computation**
- Significantly decreases training and processing times
- Captures subtle details that sequential processing may miss
- Enables training of [[Large Language Model|Large Language Models]] like GPT and BERT

### Applications

- Signal processing
- Image processing
- Natural language processing
- Machine translation
