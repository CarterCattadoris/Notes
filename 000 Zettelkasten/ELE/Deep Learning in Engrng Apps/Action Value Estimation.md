202602261001
Status: #idea
Tags: [[Reinforcement Learning]], [[Deep Learning (ELE400)]]

**Action Value Estimation** is the method of estimating the expected reward of taking a particular action in [[Reinforcement Learning]].

## Sample-Average Method

The estimated value of action $a$ at the $t$-th time step, having been chosen $N_t(a)$ times, is the average of all rewards received:

$$Q_t(a) = \frac{R_1 + R_2 + \cdots + R_{N_t(a)}}{N_t(a)}$$

- $R_i$: The actual reward received on the $i$-th selection of action $a$.
- $Q_t(a)$: The estimated value (expected reward) of action $a$ at time $t$.

As $N_t(a) \to \infty$, $Q_t(a)$ converges to the true action value $q(a)$ by the law of large numbers.

## Usage

The action value estimate is used by the [[Epsilon-Greedy Method]] and other action selection strategies to determine the greedy action:
$$A_t^* \text{ for which } Q_t(A_t^*) = \max_a Q_t(a)$$

Keeping the full history of rewards can be cumbersome, which motivates the [[Incremental Update Rule]].
