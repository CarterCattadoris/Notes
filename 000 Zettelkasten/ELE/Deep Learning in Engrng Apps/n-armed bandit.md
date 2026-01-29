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
