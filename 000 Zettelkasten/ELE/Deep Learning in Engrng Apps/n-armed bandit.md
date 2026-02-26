202601291509
Status: #idea
Tags: [[Reinforcement Learning]], [[Probabilistic Models]]

The **n-armed bandit problem** (named after the "one-armed bandit" slot machine) is a classic example used to demonstrate the [[Exploration vs Exploitation]] dilemma.

## The Problem
-   You are faced with $n$ different options (actions/levers).
-   You do not know the expected payout (value) of each action.
-   You have estimates of the values based on past trials ($t$).

## Strategies
1.  **Greedy Action**: Always choose the lever with the highest estimated value. This is **exploitation**.
2.  **Non-Greedy Action**: Choose a lever with a lower estimated value to gather more data. This is **exploration**.

The problem seeks a strategy to balance these choices to maximize total payout over many trials.

## Formal Setup
- Action values $q(a)$ for $a = 1, \ldots, n$ are unknown.
- The agent estimates values using [[Action Value Estimation]]: $Q_t(a)$.
- The [[Epsilon-Greedy Method]] is a practical solution: be greedy most of the time, explore with probability $\varepsilon$.

## Simulation Example
A set of 2000 randomly generated 10-armed bandit tasks were simulated. Action values $q(a)$ were drawn from $\mathcal{N}(0, 1)$. On each step, the actual reward was $q(A_t)$ plus Gaussian noise $\mathcal{N}(0, 1)$. Results over 1000 steps showed $\varepsilon = 0.1$ outperforms $\varepsilon = 0.01$, which outperforms $\varepsilon = 0$ (pure greedy).
