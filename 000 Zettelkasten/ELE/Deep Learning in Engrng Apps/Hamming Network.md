202601271508
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Unsupervised Learning]]

The **Hamming Network** is a competitive learning network that selects the stored pattern with the minimum [[Hamming Distance]] to the input pattern. It is designed effectively as a maximum likelihood classifier for binary patterns corrupted by noise.

## Architecture
As defined in *Deep Learning in Engineering Applications*, the network consists of:
1.  **Feedforward Layer (Matching Scores)**:
    -   Computes inner products (correlation) between input and stored patterns.
    -   Weights are derived directly from the exemplar patterns.
2.  **Recurrent Layer ([[Maxnet]])**:
    -   A recurrent competition layer that iteratively suppresses weaker signals until only the "winner" (closest match) remains.

## Weight & Bias Definitions
For an input vector $\mathbf{i}$ and stored patterns $\mathbf{e}^1, \dots, \mathbf{e}^P$:

### Weight Matrix
The weights are defined as half the transposed exemplar matrix:
$$ W = \frac{1}{2} \begin{pmatrix} \mathbf{e}^1 \\ \vdots \\ \mathbf{e}^P \end{pmatrix} $$
Or specifically for the connection to node $j$ from input $k$:
$$ w_{jk} = \frac{e^j_k}{2} $$

### Threshold (Bias)
The bias vector $\theta$ is set to negative half the dimension ($n$) of the input:
$$ \theta = -\frac{n}{2} $$

*Note: This specific bias formulation aligns the output range such that a perfect match yields an output of $n/2 - (-n/2) = n$? No, let's verify:*
Original Equation: $\mathbf{y} = \mathbf{W}\mathbf{x} + \theta$.
If $\mathbf{x} = \mathbf{e}^j$ (perfect match), $\mathbf{x} \cdot \mathbf{e}^j = n$.
Then $y = \frac{n}{2} - \frac{n}{2} = 0$? 
Wait, the original note had: $\theta = -\frac{1}{2} \begin{pmatrix} n \\ \dots \\ n \end{pmatrix}$.
Let's stick EXACTLY to the presentation's formula from the original note:
$$ \theta = -\frac{1}{2} \begin{pmatrix} n \\ \vdots \\ n \end{pmatrix} $$

## Operation
1.  **Initialize**: Apply input $i_p$ to the lower layer.
2.  **Matching Score**: Calculate initial outputs $y_j(0)$:
    $$ y_j = \sum_{k=1}^n w_{jk} i_{p,k} + \theta_j $$
    This value corresponds to the number of matching bits minus constant offsets.
3.  **Competition**: Feed $y_j(0)$ into the [[Maxnet]].
    -   The [[Maxnet]] iterates until only one positive node remains.
    -   The winning node corresponds to the stored pattern $\mathbf{e}^j$ closest to the input.

## Example
Stored patterns:
$\mathbf{e}^1 = [1, -1, -1, 1]$
$\mathbf{e}^2 = [1, -1, 1, 1]$

Weights:
$W = \frac{1}{2} \begin{pmatrix} 1 & -1 & -1 & 1 \\ 1 & -1 & 1 & 1 \end{pmatrix}$

Bias ($n=4$):
$\theta = -\frac{1}{2} [4, 4]^T = [-2, -2]^T$

If Input $\mathbf{x} = [1, -1, -1, 1]$ (Matches $\mathbf{e}^1$):
$y_1 = \frac{1}{2}(1 + 1 + 1 + 1) - 2 = 2 - 2 = 0$.
$y_2 = \frac{1}{2}(1 + 1 - 1 + 1) - 2 = 1 - 2 = -1$.
Maxnet input: $[0, -1]$. Winner: Node 1.

---
### References
- [[Maxnet]]
- [[Hamming Distance]]