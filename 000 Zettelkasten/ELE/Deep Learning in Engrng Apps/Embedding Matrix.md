202602261020
Status: #idea
Tags: [[Transformer]], [[Deep Learning (ELE400)]]

An **Embedding Matrix** is a lookup table that maps every word in a lexicon to a high-dimensional numerical vector (an **embedding**). It is the core data structure of the [[Input Embedding Layer]].

## Structure

- Each row corresponds to a word in the vocabulary.
- Each column is one dimension of the embedding space.
- Typical dimensions: ~300 (e.g., a 50,000-word vocabulary produces a 50,000 x 300 matrix).
- Storage example: 50,000 x 300 x 4 bytes (floats) = ~60 MB.

## Learning Meaning

- Words that appear in similar contexts (e.g., "worker", "fisherman", "dog" in "when the ___ left") develop similar embeddings.
- Relationships between words can be represented by mathematical operations on their embedding vectors (e.g., the difference between vectors).
- These relationships are **not commutative**: the relationship W~F is not the same as F~W.

## Training

- The embedding matrix is **randomly initialized**.
- It is trained via **self-supervised learning**: the model learns to predict context from words (continuous bag of words) or the next word in a sequence (causal model).
- Training uses [[Gradient Descent]] to minimize prediction error.
- Dimensions in the embedding do not have predefined labels; their meaning emerges from training.

## Vocabulary Size

- The number of rows is finite and depends on the context and language richness.
- Rarely used words may be excluded from the matrix.
