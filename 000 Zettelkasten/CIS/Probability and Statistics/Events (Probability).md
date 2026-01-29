202601291300
Status: #idea
Tags: [[Probability and Statistics (CIS321)]]

An **event** is a subset of a [[Sample Spaces|sample space]]. Events represent outcomes of interest in a probability experiment.

## Definition

For sample space $\Omega$, an event $A \subseteq \Omega$.

## Example: Die Toss

Sample space: $\Omega = \{1, 2, 3, 4, 5, 6\}$

- Event A (odd): $A = \{1, 3, 5\}$
- Event B (even): $B = \{2, 4, 6\}$

## Set Operations on Events

### Disjoint Sets
Events with no common outcomes. Lead to [[Unconditional Probability|unconditional probability]].

$$A \cap B = \emptyset$$

### Intersection
Common outcomes between events.

$$A \cap B = \{\text{outcomes in both } A \text{ and } B\}$$

### Union
All outcomes in either event.

$$A \cup B = \{\text{outcomes in } A \text{ or } B\}$$

### Complement
All outcomes NOT in the event.

$$A^c = \Omega \setminus A$$

**Key identity:**
$$A \cup A^c = \Omega$$

## Probability of Complement

$$P(A) = 1 - P(A^c)$$

## Addition Rule

For any events A and B:
$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

For disjoint events ($A \cap B = \emptyset$):
$$P(A \cup B) = P(A) + P(B)$$

## Connection to Set Theory

Events are fundamentally [[Sets|sets]], and event operations are [[Set Operations|set operations]]:
- Event intersection ↔ [[Intersection]]
- Event union ↔ [[Unions]]
- Event complement ↔ [[Set Difference]]
- Disjoint events ↔ Disjoint sets

---
### References
- Day 2 Lecture notes (CIS321)
- [[Discrete Math (CIS375)]] - Set theory foundations
