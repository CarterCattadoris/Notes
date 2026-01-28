202601281154
Status: #idea
Tags:[[CIS 321]]

A fair die is thrown twice. A is the event "sum of the throws equals 4" and B is "at least one of the throws is a 3"

calculate $P(A | B)$
$P(A) = \frac{3}{36} = \frac{1}{12}$
$P(B) = \frac{12}{36} = \frac{1}{3}$
$P(A|B) = \frac{P(A \cap B)}{P(B)} = \frac{\frac{2}{36}}{\frac{12}{36}} = \frac{1}{18}$
$P(A \cap B) = \{ (1,3), (3,1) \} = \frac{2}{36}$

Are A and B independent events?
no, $P(A) \neq P(A|B)$

We draw 2 cards from a deck of 52. Let $S_{1}$ be the event the first one is a spade and $S_{2}$ is the second one is a spade

Compute $P(S_{1}),P(S_{2}|S_{1})$, and $P(S_{2}| S_{1}^C)$
$P(S_{1}) = \frac{13}{52} = \frac{1}{4}$
$P(S_{2}|S_{1}) = 12/51$, given s1 happened what is the probability of s2
$P(S_{2}| S_{1}^C) = \frac{13}{51}$

calculate $P(S_{2})$ depending on whether the first card is a spade
$P(S_{2}\cap S_{1}) + P(S_{2} \cap S_{1}^C)$, the first card either is or isnt a spade
$= P(S_{2}|S_{1}) \cdot P(S_{1}) + P(S_{2}| S_{1}^C) \cdot P(S_{1}^C)$ = $\frac{12}{51} \cdot \frac{1}{4} + \frac{13}{51} \cdot \frac{3}{4} = \frac{1}{4}$


C: student answers correctly
K: student knows the answer

$P(K | C) = \frac{P(K \cap C)}{P(C)} = \frac{P(C|K)\cdot P(K)}{ P(C)}$
$P(C|K) = 1$
$P(C|K^C) = \frac{1}{4}$
$P(K) = 0.6$
$P(C) = P(C \cap K) + P(C \cap K^C)$
= $P(C|K) \cdot P(K) + P(C|K^C) \cdot P(K)$
-> $1 \cdot 0.6 + \frac{1}{4} \cdot 0.4$
-> $P(C) = 0.7$
