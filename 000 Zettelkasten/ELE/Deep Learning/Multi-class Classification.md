202601281015
Status: #idea
Tags: [[Deep Learning (ELE400)]]

Classification with more than two classes

### Approaches

**Multiple Binary Classifiers**
- Use multiple [[Perceptron]] units
- Each separates one class from others
- Combine decisions

**Multi-layer Network**
- Data format: $(a_i, b_i, c)$ where $c \in \{1, 2, 3, ...\}$
- Network learns decision boundaries between all classes

### Non-numeric Classes
For classes like {red, green, blue, black}:
- Assign numeric labels: red=1, green=2, blue=3, black=4
- Or use one-hot encoding

### Classification Types
1. [[Binary Classification]] - two classes
2. Multi-class (Label) - multiple exclusive classes
3. Fuzzy/Probabilistic - membership grade $\in [0, 1]$

---
### References
