[[Truth Tables]]
Question 1:

| q   | r   | s   | $(q \lor r)$ | $((q \lor r) \rightarrow s)$ | $(q \land r)$ | $((q \lor r) \rightarrow s) \leftrightarrow (q\land r)$ |
| --- | --- | --- | ------------ | ---------------------------- | ------------- | ------------------------------------------------------- |
| T   | T   | T   | T            | T                            | T             | T                                                       |
| T   | T   | F   | T            | F                            | T             | F                                                       |
| T   | F   | T   | T            | T                            | F             | F                                                       |
| T   | F   | F   | T            | F                            | F             | T                                                       |
| F   | T   | T   | T            | T                            | F             | F                                                       |
| F   | T   | F   | T            | F                            | F             | T                                                       |
| F   | F   | T   | F            | T                            | F             | F                                                       |
| F   | F   | F   | F            | T                            | F             | F                                                       |

Question 2:

| p   | q   | r   | $\neg q$ | $(p \rightarrow \neg q)$ | $\neg(p \rightarrow \neg q)$ | $\neg r$ | $(\neg r \lor q)$ | $\neg(p \rightarrow \neg q) \leftrightarrow  (\neg r \lor q)$ |
| --- | --- | --- | -------- | ------------------------ | ---------------------------- | -------- | ----------------- | ------------------------------------------------------------- |
| T   | T   | T   | F        | F                        | T                            | F        | T                 | T                                                             |
| T   | T   | F   | F        | F                        | T                            | T        | T                 | T                                                             |
| T   | F   | T   | T        | T                        | F                            | F        | F                 | T                                                             |
| T   | F   | F   | T        | T                        | F                            | T        | T                 | F                                                             |
| F   | T   | T   | F        | T                        | F                            | F        | T                 | F                                                             |
| F   | T   | F   | F        | T                        | F                            | T        | T                 | F                                                             |
| F   | F   | T   | T        | T                        | F                            | F        | F                 | T                                                             |
| F   | F   | F   | T        | T                        | F                            | T        | T                 | F                                                             |

Question 3: 
1. Q1 and Q4 are logically equivalent to each other because their values are the same in every row of the truth table
2. Q6 is the only one on the chart that is logically consequent of Q2 because it is the only one on the chart that is always true when Q2 is true


Question 4:

| p   | q   | r   | $p \land q$ | $(p \land q) \to r$ | $r \to q$ | $p \to q$ | $\neg(p \to q)$ | $\neg r$ | $\neg r \lor p$ | $q \to (\neg r \lor p)$ |
| --- | --- | --- | ----------- | ------------------- | --------- | --------- | --------------- | -------- | --------------- | ----------------------- |
| T   | T   | T   | T           | T                   | T         | T         | F               | F        | T               | T                       |
| T   | T   | F   | T           | F                   | T         | T         | F               | T        | T               | T                       |
| T   | F   | T   | F           | T                   | F         | F         | T               | F        | T               | T                       |
| T   | F   | F   | F           | T                   | T         | F         | T               | T        | T               | T                       |
| F   | T   | T   | F           | T                   | T         | T         | F               | F        | F               | F                       |
| F   | T   | F   | F           | T                   | T         | T         | F               | T        | T               | T                       |
| F   | F   | T   | F           | T                   | F         | T         | F               | F        | F               | T                       |
| F   | F   | F   | F           | T                   | T         | T         | F               | T        | T               | T                       |

1. is $q \to (\neg r \lor p)$ a logical consequence of $p \to q$ and $\neg r$? Explain
	1. Yes it is a logical consequence because at every instance that $p \to q$ and $\neg r$ are true, $q \to (\neg r \lor p)$ is true
2. Which of the formulas in the set $[p ∧ q, r → q, q → (¬r ∨ p)]$ are logical consequences of $(p ∧ q) → r, p → q, and ¬r$? Explain your answer.  
	1. In rows 6 and 8 where the three listed statements are true, $[r → q, q → (¬r ∨ p)]$ are both true therefore they are both logical consequences of the listed statements 
3. Explain why F (i.e., false) is a logical consequence of $p ∧ q$ and $¬(p → q)$
	1. False is a logical consequence of the 2 listed statements because there is no row in the truth table for which both have a value of true