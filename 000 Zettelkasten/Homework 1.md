202602181140
Status: #idea
Tags:[[Probability and Statistics (CIS321)]]

# Problem 1 — Quality Control Testing [40 pts]
A factory produces microchips from two production lines:
• Line A produces 60% of all chips.
• Line B produces 40% of all chips.
Each chip is tested for defects. Historical data shows:
• Probability a chip from Line A is defective: 3% $P(D | A)$
• Probability a chip from Line B is defective: 7% $P(D | B)$
Notation to use (define your events clearly): Either label your notations clearly for each
event and probability, or use the following event symbols in your work:
• A: the selected chip came from Line A;
• B: the selected chip came from Line B.
• D: the selected chip is defective;
• Dc: the selected chip is non-defective.
• Probabilities should be written using symbols such as $P (A), P (D | A), P (A | D) P (B ∩ D^c)$.

## Tasks
P1.1 Define the sample space for the experiment “randomly select a chip and observe (a) its production line and (b) whether it is defective.” [6 pts]
$$S = \{ (A,D), (A, D^c), (B, D), (B, D^c) \}$$
P1.2 Compute the probability that a randomly selected chip is defective. [8 pts]
$P(D) = P(D \cap A) +  P(D \cap B) = P(D|A) \cdot P(A) + P(D | B) \cdot P(D)$
$= 0.03 \cdot 0.6 + 0.07 \cdot 0.4 = 0.046 = 4.6\%$
P1.3 Compute the probability that a randomly selected chip is non-defective and came from Line B. [6 pts]
$P(D^c | B) = 1-P(D|B) = 0.93$
$P(D^c \cap B) = P(D^c | B) \cdot P(B) = 0.372 = 37.2\%$
P1.4 A randomly selected chip is found to be defective. [14 pts]
(a) Compute the probability it came from Line A (use Bayes’ rule). [10 pts]
$P(A|D) = \frac{P(A \cap D)}{P(D)} = \frac{P(D | A) \cdot P(A)}{P(D)} = \frac{0.03 \cdot 0.6}{0.046} = 0.3913 = 39.13\%$
(b) Interpret this probability in context. [4 pts]
Even though line A produces 60% of the 
P1.5 Are the events “chip is from Line A” and “chip is defective” independent? Justify your
answer mathematically using the definition of independence. [6 pts]