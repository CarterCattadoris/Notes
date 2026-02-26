202602261033
Status: #idea
Tags: [[Deep Learning (ELE400)]]

## Content

**Data Preprocessing** transforms raw input data before feeding it to a neural network to improve training stability and convergence.

### Mean Subtraction

Subtract the mean across every individual input variable (feature):

$$x' = x - \bar{x}$$

- Centers the data around zero.
- Prevents bias toward features with large absolute values.

### Normalization

Divide each zero-centered feature by its standard deviation:

$$x'' = \frac{x'}{\sigma}$$

- Scales all features to comparable ranges.
- Prevents features with large variance from dominating learning.

### Pipeline

Original data $\rightarrow$ Zero-centered data (mean subtraction) $\rightarrow$ Normalized data (divide by $\sigma$).

### Relation to Other Normalization

- [[Min-Max Normalization]] scales values to a specific range $[n_{\min}, n_{\max}]$.
- Standard normalization (above) produces zero mean with unit variance.
- Both aim to ensure consistent input ranges for stable [[Gradient Descent]].
