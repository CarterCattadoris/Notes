202601291415
Status: #idea
Tags: [[Deep Learning (ELE400)]], [[Unsupervised Learning]]

The **Simple Competitive Learning Network** extends the topology of the [[Hamming Network]] to handle real-valued inputs instead of binary ones.

## Key Differences from Hamming Network
-   **Input**: Real values ($\mathbb{R}^n$) instead of binary/bipolar.
-   **Weights**: Real-valued vectors.
-   **Operation**: Finds the weight vector closest to the input vector (often using Euclidean distance or dot product).

## Architecture
1.  **Input Layer**: Receives real-valued pattern $\mathbf{x}$.
2.  **Competitive Layer**:
    -   Calculates similarity (e.g., dot product $\mathbf{w}_j \cdot \mathbf{x}$).
    -   Selects a winner (Winner-Take-All).
    -   **Winning Output** = 1 (or active).
    -   **Others** = 0 (or inactive).

---
### References
- [[Hamming Network]]
- [[Maxnet]]
