202601291415
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Unsupervised Learning]]

The **Simple Competitive Learning Network** extends the topology of the [[Hamming Network]] to handle real-valued inputs instead of binary ones.

## Key Differences from Hamming Network
-   **Input**: Real values to real values. The input vectors change from binary $\{-1, +1\}$ to real-valued range $[-1, +1]$.
-   **Weights**: Real-valued vectors ($W_{j,l}$).
-   **Operation**: Finds the weight vector closest to the input vector (often using Euclidean distance or dot product).

## Architecture
1.  **Input Layer**: Receives real-valued pattern $\mathbf{i}_k$ (k-th input pattern).
2.  **Competitive Layer**:
    -   Calculates similarity/distance.
    -   Selects a winner $j^*$ (closest output node) using [[Maxnet]].
    -   **Winning Output** = 1.
    -   **Others** = 0.

## Learning Rule
When the winning node $j^*$ is found for input $i_{k}$, the weights for that node are updated to move closer to the input pattern:

$$ \Delta w_{j^*, l} = \eta (i_{k, l} - w_{j^*, l}) $$

for $l \in \{1, 2, \dots, n\}$.
*   $\eta$: Learning rate.
*   The update only affects the winning neuron (Winner-Take-All). 

---
### References
- [[Hamming Network]]
- [[Maxnet]]
- Lecture Notes 260129
