202502271141
Status: #idea
Tags:[[Equivalence Relations]]

Let R be an [[Equivalence Relations]] on the set A, and let $w ∈ A$.  
The equivalence class of w under R (written $[w]_R$ ) is the set of elements  in A that R relates to w :  
$[w]_R = \{z ∈ A : (w , z) ∈ R\}$.  
Each $z ∈ [w]_{R}$ is said to be a representative of the class $[w]_{}R$ 

## Example
The relation S has three distinct equivalence classes:  $S = \{ (1, 1), (2, 2), (3, 3), (4, 4), (5, 5), (2, 3), (3, 2), (2, 4), (4, 2), (3, 4), (4, 3) \}$
$[1]_S = {1}$
$[2]_S = \{2, 3, 4\} = [3]_{S} = [4]_{S}$
$[5]_{S} = \{5\}$

Let B be the following set of bit strings:  
$B = \{0010, 1010, 1100, 10011, 01001, 11011\}$
1. Define R1 to be the following relation on B:  
$R_1 = \{(b1, b2)$ : the length of b1 is less than or equal to the length of b2}  
R1 is not an equivalence relation. Explain why not by explicitly identifying how one of the three essential properties fails to hold. 

$R_{1}$ is not symmetric because $(0010,10011) \in R_{1}$ but $(10011,0010) \not\in R_{1}$

1. Define $R_{2}$ to be the following relation on B:  
$R_{2} = \{(b_{1}, b_{2}) : b_{1} \space and \space b_{2}$ contain exactly the same number of 0s}  
$R_{2}$ is an equivalence relation. Give $R_{2}$’s equivalence classes.

$\{ 0010, 01001 \}$ 
$\{11011\}$
$\{1010, 1100,10011 \}$
