202601281019
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Density-Based Spatial Clustering of Applications with Noise - a [[Clustering]] algorithm

### Parameters
- **Eps** ($\epsilon$): radius of neighborhood
- **MinPts**: minimum points within Eps to form a dense region

### Point Types
1. **Core points**: have $\geq$ MinPts neighbors within Eps
2. **Border points**: near core points but lack enough neighbors
3. **Noise points**: don't belong to any cluster

### Advantages over K-Means
- Can find arbitrarily shaped clusters
- Automatically identifies noise/outliers
- No need to specify number of clusters

### Example
With MinPts=4 and eps=1 unit:
- Points with 4+ neighbors in radius 1 are core points
- Points near core points with fewer neighbors are border points
- Isolated points are noise

### When to Use
- Data has non-spherical clusters
- Clusters have varying densities
- Need to identify outliers

---
### References
