202601281025
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Partitioning of space where each region contains all points closest to a particular center

### Definition
Given a set of center points (codewords) $\{y_1, y_2, ..., y_n\}$:

$$V_i = \{x : d(x, y_i) \leq d(x, y_j) \text{ for all } j \neq i\}$$

### Properties
- Each point belongs to exactly one region
- Regions are convex polygons
- Boundaries are perpendicular bisectors between centers

### Decision Rule
For input $x$:
- Calculate distance $d_i$ to each centroid
- If $d_1 < d_2$, then $x \in$ cluster 1

### Applications
- [[K-Means Algorithm]] - clusters form Voronoi regions
- [[Vector Quantization]] - codewords define regions
- [[Competitive Learning Network]] - neurons represent regions
- Nearest neighbor classification

---
### References
