202601281020
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Distance metric for binary vectors - counts differing bit positions

$$H(i_1, i_2) = \text{number of bits where } i_{1,j} \neq i_{2,j}$$

### Example
$i_1 = 1, 0, 1, 0$
$i_2 = 1, 1, 0, 1$
$H(i_1, i_2) = 3$ (positions 2, 3, 4 differ)

### Properties
- Range: $[0, n]$ for n-bit vectors
- $H = 0$: identical vectors
- $H = n$: completely opposite vectors

### Applications
- Error detection/correction in coding theory
- [[Hamming Network]] for pattern recognition
- Binary [[Clustering]]

---
### References
