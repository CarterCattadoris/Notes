202601281005
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Error metric used in [[Supervised Learning]] to measure prediction quality

$$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - f(x_i))^2$$

Where:
- $y_i$ is the desired (actual) output
- $f(x_i)$ is the predicted output
- $n$ is the number of samples

### Why Squared Error?
Three advantages:
1. Eliminates +/- sign cancellation
2. Punishes larger errors more heavily
3. Easy to differentiate (needed for [[Gradient Descent]])

### In Neural Networks
For a neuron with output $y$ and desired output $d$:
$$e = y - d$$
$$e^2 = (y - d)^2$$

This is minimized during training using [[Gradient Descent]]

---
### References
