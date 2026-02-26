202602261021
Status: #idea
Tags: [[Transformer]], [[Deep Learning (ELE400)]]

**Cross-Entropy Loss** is a loss function used to train models that predict probability distributions, such as next-word prediction in [[Transformer]] models.

## Information Theory Background

**Shannon Entropy** measures uncertainty in a distribution:
$$H(x) = -\sum p(x) \log_2 p(x)$$

**Cross-Entropy** between a true distribution $p$ and a predicted distribution $q$:
$$H(p, q) = -\sum_{x \in \mathcal{X}} p(x) \log q(x)$$

## Cross-Entropy Loss Formula

$$L_{CE}(\hat{\mathbf{y}}_t, \mathbf{y}_t) = -\sum_{w \in V} \mathbf{y}_t[w] \log \hat{\mathbf{y}}_t[w]$$

- $\hat{\mathbf{y}}_t$: predicted probability distribution over vocabulary.
- $\mathbf{y}_t$: true distribution (one-hot encoded).
- $V$: vocabulary.

## Simplification for Next-Word Prediction

Since the true label is one-hot ($\mathbf{y}_t[w_{t+1}] = 1$, all others 0), the loss simplifies to:
$$L_{CE}(\hat{\mathbf{y}}_t, \mathbf{y}_t) = -\log \hat{\mathbf{y}}_t[w_{t+1}]$$

This means the loss is simply the negative log probability the model assigns to the correct next word.

## Self-Supervised Learning

In a **causal model** (next-word prediction), training data is generated automatically from text sequences. The error between the generated next word and the actual next word provides the training signal, enabling self-supervised learning.
