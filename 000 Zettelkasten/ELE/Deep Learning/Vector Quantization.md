202601281024
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Technique that divides input space into [[Voronoi Regions]], each represented by a codeword

### Concept
- Like A/D conversion for multidimensional data
- Quantization not equally spaced - adapts to data distribution
- Each region represented by a single vector (codebook vector)

### Algorithm
1. Determine number of codewords $N$
2. Select $N$ codewords randomly or assign random values
3. Using Euclidean distance, cluster vectors around each codeword
4. Compute new codewords as cluster centroids
5. Repeat until convergence

### Applications
- Data compression
- Image coding
- Speech coding
- Pattern recognition

### Relation to Clustering
Essentially [[K-Means Algorithm]] where:
- K = number of codewords
- Centroids = codewords
- Clusters = Voronoi regions

---
### References
