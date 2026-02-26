202602261000
Status: #idea
Tags: [[Reinforcement Learning]], [[Deep Learning (ELE400)]]

The **Epsilon-Greedy Method** ($\varepsilon$-greedy) is a strategy for balancing [[Exploration vs Exploitation]] in [[Reinforcement Learning]].

## Mechanism

The agent selects the **greedy action** (the action with the highest estimated value) most of the time, but with a small probability $\varepsilon$, it instead selects a **random non-greedy action**.

$$P(\text{non-greedy action}) = \varepsilon$$
$$P(\text{greedy action}) = 1 - \varepsilon$$

The greedy action $A_t^*$ is defined as:
$$A_t^* \text{ for which } Q_t(A_t^*) = \max_a Q_t(a)$$

where $Q_t(a)$ is the [[Action Value Estimation]] at time step $t$.

## Effect of $\varepsilon$

Simulations on 2000 randomly generated 10-armed bandits show:
- $\varepsilon = 0.1$: Highest average reward and ~80% optimal action selection after 1000 steps. Explores frequently, discovers best actions fastest.
- $\varepsilon = 0.01$: Slower improvement, reaches ~50% optimal action selection. Explores less, converges slower but with less noise.
- $\varepsilon = 0$ (pure greedy): Lowest performance, stuck at ~33% optimal action. Gets trapped exploiting a suboptimal action early on.

Higher $\varepsilon$ leads to more exploration and faster discovery of optimal actions, at the cost of more random (non-greedy) moves during execution.
