202602261002
Status: #idea
Tags: [[Reinforcement Learning]], [[Deep Learning (ELE400)]]

The **Incremental Update Rule** provides an efficient way to update [[Action Value Estimation]] without storing the full history of rewards.

## Derivation

Starting from the sample-average definition:
$$Q_{k+1} = \frac{1}{k} \sum_{i=1}^{k} R_i = \frac{1}{k}\left(R_k + \sum_{i=1}^{k-1} R_i\right)$$

Substituting $(k-1)Q_k$ for the partial sum:
$$Q_{k+1} = \frac{1}{k}\left(R_k + (k-1)Q_k\right) = Q_k + \frac{1}{k}\left[R_k - Q_k\right]$$

## General Form

$$\text{NewEstimate} \leftarrow \text{OldEstimate} + \text{StepSize}\left[\text{Target} - \text{OldEstimate}\right]$$

$$Q_{k+1} = Q_k + \alpha\left[R_k - Q_k\right]$$

- $Q_k$: Current estimate (OldEstimate)
- $R_k$: Actual reward received (Target)
- $\alpha$: Step size parameter
- $R_k - Q_k$: The **error** between actual reward and estimated reward

## Connection to Supervised Learning

The step size $\alpha$ in RL plays the same role as the [[Learning Rate]] $\eta$ in [[Supervised Learning]]. Both control how much new information updates the current estimate.
