## Part 1
Suppose the following sets are defined:
M = {3, 7, 9, 2}
P = {6, 7, 2, 8, 4}
Q = {{3}, 7, {}}
S = {4, 1}
T = {5, 9, 3}
V = {y ∈ N | y|60}
1. $S \cap P=\{4\}$
2. $M\cap Q=\{ 7 \}$
3. $P \cup M = \{ 6,3,7,9,2,8,4 \}$
4. $M-T=\{ 7,2 \}$
5. $P-(S\cup M)=\{ 6,8 \}$
6. $\{ v \in V |$ v is odd} = {1,3,5,15}
7. $S \times T$ = {(4,5), (4,9), {4,3), (1,5), (1,9), (1,3)}
8. $M \triangle P$ = {3, 9, 6, 8, 4}
9. $2^S$ = {$\emptyset$, {4}, {1}, {4,1}}
10. $2^\emptyset$ = {$\emptyset$}
11. |Q| = 3
12. $|2^M|$ = $2^4$  

## Part 2
For each of the following, find sets D and F that satisfy the indicated constraints. For each one, explicitly spell out the constraints that must be satisfied as well as your answers for D and F .

1. D − F = {5, 9, 3}, F − D = {6, 2}, and D ∩ F = {7, 8} --> D = {5,9,3,7,8} , F = {6,2,7,8}
	1. Constraints: 
		1. 5,9,3 are in D but not in F
		2. 6,2 are in F but not in D
		3. 7,8 are in D and F
2. |D ∩ F| = |D − F | = 4 --> D = {1,2,3,4,5,6,7,8}, F = {5,6,7,8,9,10,11,12}
	2. Constraints:
		4. sets D∩F and D-F both have 4 elements
3. |F × D| = 15 and |D| < |F| --> D = {1,2,3}, F = {4,5,6,7,8}
	1. Constraints: 
		1. F x D has 15 elements, F has more elements then D
4. D ∈ F and D ⊆ F --> D = {1}, F = {1,{1}} 
	2. Constraints:
		2. D is an element of F
		3. every element of D is an element of F
5. $F ∈ 2^D$ and $D \neq F$ and 4 ∈ D --> D = {4}, F = $\emptyset$
	1. Constraints:
		1. F is in the powerset of D(in the subsets of D)
		2. D is not the same set as F
		3. 4 is an element of D

## Part 3
A small technology firm PicoTech has several ongoing projects, the most lucrative of which
are its Lambda and Kappa projects.
For this question, consider the following sets of PicoTech employees (people may belong to
more than one set):
• W : the set of PicoTech employees who are very well paid
• P : the set of PicoTech employees who are programmers
• L : the set of PicoTech employees who are assigned to the Lambda project
• K : the set of PicoTech employees who are assigned to the Kappa project
• J : the set of PicoTech employees who know Java well

i. Express each of the following English statements using the language of set theory:
1. Every very-well paid employee at PicoTech is assigned to at least one of the Kappa and Lambda projects.
	$W \subseteq(K \cup L)$
7. There is at least one very well paid PicoTech programmer who is assigned to the Kappa project but does not know Java well.
	$W \cap K \nsubseteq J$
8. None of the very-well paid PicoTech employees assigned to the Lambda project know Java well.
	$(W \cap L \cap J) = \emptyset$
9. PicoTech has more very well paid employees than it has programmers who know Java well.
	$|W| > |P \cup J|$

ii. Express each of the following set-theory statements in everyday (but unambiguous)
English (include the set-theory notation as part of your answer):
1. $W \nsubseteq(L ∩ P )$ 
	At least one of the very-well paid PicoTech employees are assigned to the lamda project and are programmers
11. $J ⊆ K − L$
	Every PicoTech employee who knows java well is assigned to the kappa project but not assigned to the lambda project
12. $(K ∪ L) = P \triangle W$ 
	 The Picotech employees who are assigned to the kappa project or assigned to the lambda project (or both) are the same as Picotech employees who are programmers or well paid (but not both)