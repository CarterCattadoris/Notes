202601271508
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Unsupervised Learning]]

The **Hamming Network** is a competitive learning network that selects the stored pattern with the minimum [[Hamming Distance]] to the input pattern. It acts as a maximum likelihood classifier for binary patterns corrupted by noise.

## Architecture
1.  **Feedforward Layer**: Computes matching scores (correlation) between input and stored patterns.
2.  **Recurrent Layer ([[Maxnet]])**: Iteratively finds the winner (closest match).

## Parameters
For input dimension $n$ and stored patterns $\mathbf{e}^1 \dots \mathbf{e}^P$:

### Weights & Bias
$$ W = \frac{1}{2} \begin{pmatrix} \mathbf{e}^1 \\ \vdots \\ \mathbf{e}^P \end{pmatrix} $$
$$ \theta = -\frac{1}{2} \begin{pmatrix} n \\ \vdots \\ n \end{pmatrix} $$

### Output Calculation
Consider that a new input pattern vector $\mathbf{i}$ is applied to the input. Then the output vector $\mathbf{o}$ can be found as:

$$ \mathbf{o} = W \mathbf{i} + \theta = \begin{pmatrix} \frac{1}{2} \mathbf{e}^1 \cdot \mathbf{i} - \frac{n}{2} \\ \vdots \\ \frac{1}{2} \mathbf{e}^P \cdot \mathbf{i} - \frac{n}{2} \end{pmatrix} $$

This represents the correlation between the input and each stored pattern, shifted by the bias.

## Example 1: Hamming Weights & Scores (Notes260129)
**Stored Patterns** ($n=5$):
$\mathbf{e}^1 = [1, -1, -1, 1, 1]^T$
$\mathbf{e}^2 = [-1, 1, -1, 1, -1]^T$
$\mathbf{e}^3 = [1, -1, 1, -1, 1]^T$

**1. Weights ($W$)**:
$$ W = \frac{1}{2} \begin{pmatrix} 1 & -1 & -1 & 1 & 1 \\ -1 & 1 & -1 & 1 & -1 \\ 1 & -1 & 1 & -1 & 1 \end{pmatrix} $$

**2. Threshold ($\theta$)**:
$$ \theta = -\frac{1}{2} [5, 5, 5]^T = [-2.5, -2.5, -2.5]^T $$

**3. Test Input**:
$\mathbf{i} = [1, 1, 1, -1, -1]^T$

**4. Feedforward Output**:
$o_1 = \frac{1}{2}(1 - 1 - 1 - 1 - 1) - 2.5 = -4.0$
$o_2 = \frac{1}{2}(-1 + 1 - 1 - 1 + 1) - 2.5 = -3.0$
$o_3 = \frac{1}{2}(1 - 1 + 1 + 1 - 1) - 2.5 = -2.0$

## Example 2: Maxnet Convergence
The matching scores are fed into the [[Maxnet]].
**Given**: 5 nodes with initial values $(0.5, 0.9, 1.0, 0.9, 0.9)$, $\theta=1$, $\epsilon=1/5$.

**Iteration 1**:
Input to node 3 (the max) is $1.0 - 0.2(0.5 + 0.9 + 0.9 + 0.9) = 1.0 - 0.2(3.2) = 0.36$.
*Note: Maxnet typically suppresses non-max values to zero over iterations.*

In the context of Example 1, the inputs are $[-4, -3, -2]$. The Maxnet would select **Node 3** (-2.0) as the winner (closest match).

---
### References
- [[Maxnet]]
- [[Hamming Distance]]
- [[Simple Competitive Learning Network]]