202502191831
Status: #idea
Tags:[[Discrete Math (CIS375)]]
W : animals that have wings  
F : animals that fly  
T : animals that have toes  
E : animals that lay eggs  
S : animals that can sing  
C : animals that are cold-blooded  
Express each of the following English statements using the language of set theory:  
a. There are some animals with wings that neither fly nor lay eggs. 

$(W -F)-E \neq \emptyset$

b. All animals that have either wings or toes (but not both) can sing.  

$(W \triangle T) \subseteq S$

c. No animal that has toes and doesn’t fly can sing.

$(T -F) \cap S = \emptyset$ 


every animal that can sing has wings and is not cold blooded


There are some animals that lay eggs and either have toes or can fly (or both)



Consider the following definitions:  
• An integer n is gammic provided there is an integer k such that n = 5k − 2.  
• An integer n is deltic provided there is an integer k such that n = 4k + 3.  

In addition, recall the following two facts about integers:  
• Fact 1: The sum of any two integers is an integer.  
• Fact 2: The product of any two integers is an integer.  
Give a direct proof of the following claim:  
Let a and b be integers. If a is gammic and b is deltic, then 9b + 4a is deltic.

Proof:(direct)
- Let a and b be integers
- suppose a is gammic and b is deltic
- NTS: 9b + 4a is deltic
- Let c and d be integers
- By definition of deltic, b = 4c+3
- By definition of gammic, a = 5d-2
- By algebra, 9b = 9(4c+3) = 36c+27
- By algebra, 4a = 4(5d-2) = 20d-8
- By algebra, 9b+4a = 36c+27+20d-8 = (36c+20d)+19 = 4(9c+5d+16)+3
- Since c, d, and 16 are all integers, so is (9c+5d+4)
- Therefore there is an integer k(ie 9c+5d+4) such that 9b+4a = 4k+3
- Therefore 9b+4a is deltic



Let J, K, P, Q be sets. If J ⊆ Q, then (J − K) ∩ (J − P ) ⊆ Q − (K ∪ P ).

Proof:(direct)
- Suppose $J \subseteq Q$
- Consider an arbitrary element $w \in (J-K) \cap (J-P)$
- NTS: $w \in Q − (K ∪ P )$
- By definition of intersection, $w \in (J-K)$ and $w \in (J-P)$
- By definition of set difference:
	- $w \in J$
	- $w \not\in K$
	- $w \not\in P$
- Since $w \in J$ and $J \subseteq Q$, $w \in Q$
- Since w $\not\in K$ or P, $w \not\in K\cup P$ 
- Since $w \in Q$, and $w \not\in k\cup P$, through set different $w \in Q-(K\cup P)$ 
- Since w was an arbitrary element,  (J − K) ∩ (J − P ) ⊆ Q − (K ∪ P ).