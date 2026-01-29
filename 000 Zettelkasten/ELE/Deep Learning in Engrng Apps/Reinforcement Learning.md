202601291416
Status: #idea
Tags: [[Deep Learning (ELE400)]]

**Reinforcement Learning (RL)** is a computational approach to machine learning from interactions with the environment. It involves learning *what to do* (mapping situations to actions) to maximize a numerical reward signal.

## Distinguishing Features
-   **Closed Loop**: Previous actions influence future situations.
-   **No Instructions**: The learner is not told which actions to take; it must discover them.
-   **Trial and Error**: Actions are learned by trying them out and observing rewards ($R$).

## Mathematical Formulation
Based on optimum control theory and stochastic systems.

### Components
-   **State ($S$)**: Set of environment situations.
-   **Action ($A$)**: Set of possible actions.
-   **Transition Probability**:
    $$ P_a(s, s') = P(S_{t+1} = s' | S_t = s, A_t = a) $$
    The probability of moving from state $s$ to state $s'$ given action $a$.
-   **Reward**:
    $$ R_a(s, s') $$
    The immediate reward received for the transition.

### Goal: The Policy
The objective is to learn a policy $\pi$:
$$ \pi: S \times A \to [0, 1], \quad \pi(s, a) = P(A_t = a | S_t = s) $$
The policy defines the probability of taking action $a$ in state $s$ to maximize the **expected cumulative reward**.

## Key Concepts
-   **Exploration vs Exploitation**: Balancing the use of current knowledge ("greedy") vs trying new actions to find better rewards. See [[Exploration vs Exploitation]].
-   **n-armed Bandit**: A classic problem demonstrating this trade-off. See [[n-armed bandit]].

---
### Reference
- Sutton & Barto, *Reinforcement Learning: An Introduction*, 2nd Ed. [PDF](https://web.stanford.edu/class/psych209/Readings/SuttonBartoIPRLBook2ndEd.pdf)
