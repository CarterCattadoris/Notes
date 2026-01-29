202601281018
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Partition-based [[Clustering]] algorithm that groups data into K clusters

### Algorithm
1. Choose K (number of clusters)
2. Initialize K centroids randomly
3. Assign each point to nearest centroid
4. Recompute centroids as cluster means
5. Repeat steps 3-4 until convergence

### Centroid Update
$$\text{centroid}_{k+1} = \text{centroid}_k + \eta(\text{input} - \text{centroid}_k)$$

### Choosing K
- Large K: too many clusters with few points each
- Small K: meaningful clusters may be merged

### Voronoi Regions
Each cluster defines a [[Voronoi Regions|Voronoi region]] - the set of points closest to that centroid

### Limitations
- Assumes spherical clusters
- Sensitive to initialization
- Struggles with non-convex shapes

For non-convex shapes, use [[DBSCAN]]

---
### References
