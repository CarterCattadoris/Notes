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
Even though line A produces 60% of the chips, the lower defect rate of 3% means it only produces 39.13% of defective chips
P1.5 Are the events “chip is from Line A” and “chip is defective” independent? Justify your answer mathematically using the definition of independence. [6 pts]
Independant if: $P(A\cap D) = P(A) \cdot P(D)$
$P(A \cap D) = 0.018$
$P(A) \cdot P(D) = 0.0276$
$0.018 \neq 0.0276$, therefore they are NOT independant

# Problem 2

## P2.1

$S = \{(D, T_{1n }), (D, T_{1p}, T_{2p}), (D, T_{1p}, T_{2n}), (D^c, T_{1n}), (D^c, T_{1p}, T_{2p}), (D^c, T_{1p}, T_{2n})  \}$

## P2.2
$P(T_{1p} \cap T_{2p} | D^c) = P(T_{1p} | D^c) \cdot P(T_{2p} | D^c) = 0.05 * 0.03 = 0.0015$

## P2.3
$P(T_{1p} \cap T_{2p} | D) = P(T_{1p} | D) \cdot P(T_{2p} | D) = 0.9 * 0.95 = 0.0015$

## P2.4
$P(D | T_{1p} \cap T_{2p}) = \frac{P(T_{1p} \cap T_{2p}) \cdot P(D)}{P(T_{1}p \cap T_{2p})} = \frac{P(T_{1p} \cap T_{2p}) \cdot P(D)}{P(T_{1p} \cap T_{2p} | D) \cdot P(D) + P(T_{1p} \cap T_{2p} | D^c) \cdot P(D^c)} = \frac{0.855 \cdot 0.02}{(0.855 \cdot 0.02) + (0.0015)(0.98)} = 0.921$
## P2.5
They are not independant in general. However they are conditionally independant using disease status, since $P(T_{1p} \cap T_{2p} | D) = P(T_{1p} | D) \cdot P(T_{2p} | D)$ (same with $D^c$). They are not independant without conditioning on D though. Therefore they are not indepdant in general

# Theoretical questions
1. The set of all possible outcomes of a random experiment. Randomly choosing and recording a time during the day ends up being an infinitely large sample space, instead of one that you would expect to be simple
2. Mutually exclusive means 2 events cannot occur at the same time. Independant means one happening doesn't effect the probability of another. It cannot be both, since mutually exclusive events affect each others probabilities
3. $P(A | B) = \frac{P(A\cap B)}{P(B)}$. This represents the probability that A happens given that B already happened
4. Just because one event happened, the probability of the other related event happening is not affected at all
5. Medical testing like the above problem. You need to know the probability of actually having the disease given the test result, because usually it is not 100%
6. $P(A|B) = \frac{P(B|A)\cdot P(A)}{P(B)}$. This changes the probability of A once you observe B happening
7. It relates the prevelance of the disease to the probability of having the disease given that you test positive. The risk would most likely be overestimated without this
8. The relationship between the ground being wet and it currently raining are not independant since rain increases the chance that the ground is wet at a given time
9. A: a student studies for an exam. B: A student passes the exam. $P(B|A)$ is likely high, most students that study pass an exam. However, $P(A|B)$ is not necessarily high considering many students still pass even without studying
10. Each test gives new evidence which updates the probability. Multiple stages can increase or decrease the final probability