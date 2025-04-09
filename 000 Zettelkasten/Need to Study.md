
LF4 - recursive defined sets/ structural induction basis and conditionals

Consider the set A of strings, which is defined recursively as follows:  
• The string 302 is in A.  
• The string 12 is in A.  
• If u is a string in A, then the string 00uu is also in A.  
• If s and w are strings in A, then the string s11w2 is also in A.  

Thus, all elements of A are strings constructed from just four symbols: 0, 1, 2, and 3.  

1. List five elements of A.  
00302302, 001212, 30211122, 12113022, 000030230200302302
2. Suppose you were to use structural induction to prove that some property P holds of all elements of the set A.  
	• For the basis step, what would you need to show true?  
	P(302) is true, P(12) is true
	• For the inductive step, what conditional(s) would you need to show true?
	P(u) -> P(00uu), P(s) and P(w) -> P(s11w2)


RF5 - given relation, is it a function

For each of the following relations, determine whether or not it is a function and support your answer as follows:  
• If it’s a function, give its domain and its image (make sure you label your answers).  
• If it’s not a function, provide a brief but compelling explanation why not.  

1. The relation {(1, 1), (3, 3), (3, 4), (4, 4), (8, 1), (8, 8)}  
	1. not a function, 3 maps to 3 and 4
2. The relation {(a, b) ∈ A × A : a < b}, where A = {1, 3, 4, 8}  
	2. not a function, 1 maps to 3,4 and 8
3. The relation {(c, d) ∈ N × N : c = d + 1}
	1. is a function
	2. Domain: N, Image: N+1 **CHECK

RF6 - 1-1, onto, 

For each of the following functions, determine which of the listed properties it possesses:  
• If the function has the indicated property, write yes.  
• If the function does not have the indicated property, write no and provide a brief but compelling  
explanation why not.  
1. j : Z → Z × Z defined by: j(w) =  {(w, w + 1), if w < 0  : (w, w − 1), if w ≥ 0  
• 1-1 (injective):  
• onto (surjective):  
• bijective:  

2. e : N → Z+ defined by: e(w) =  w + 2, if 0 ≤ w ≤ 2  : w + 1 if w ≥ 4  : 1 if w = 3  
• 1-1 (injective):  
• onto (surjective):  
• bijective:  

3. d : N × N → N defined by: d(x, y) = x + 2y  
• 1-1 (injective):  
• onto (surjective):  
• bijective:

![[Pasted image 20250408193259.png]]
Claim 1

Proof: by mathematical induction
### Basis: 
P(1) is true because $(3 \cdot 1+1) = 4$, $\frac{1(3 \cdot 1 + 5)}{2} = \frac{8}{2} = 4$

### Inductive Step:
Suppose P(k) is true:
$$\sum_{i=1}^{k} (3i+1) = \frac{k(3k+5)}{2}$$
We NTS P(k+1) is true:
$$\sum_{i=1}^{k+1} (3i+1) = \frac{(k+1)(3(k+1)+5)}{2} = \frac{k(3k+8) + 3k+8}{2} = \frac{3k^2+11k+8}{2}$$
by algebra: 
$$\sum_{i=1}^{k+1} (3i+1) = (\sum_{i=1}^{k} (3i+1)) + 3(k+1)+1$$
$$
= \frac{k(3k+5)}{2} + 3(k+1)+1 = \frac{k(3k+5)}{2} + 3k+4 = \frac{k(3k+5)+6k+8}{2} = \frac{3k^2+11k+8}{2}
$$
Thus the conditional $P(k) \to P(k+1)$ is true

By the basis, inductive step, and IH, the statement is true