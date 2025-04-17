1. Consider the relation R1 = {(1, 1), (2, 2), (2, 4), (2, 5), (3, 3), (3, 6), (4, 4), (5, 4), (5, 5), (6, 6)}, defined on the set A1 = {1, 2, 3, 4, 5, 6}.  
Determine whether R1 is a partial order on A1 and support your answer as follows:  

• If R1 is a partial order:  
– Give all minimal elements of the poset (A1, R1) or explain why none exist.  
– Give all maximal elements of the poset (A1, R1) or explain why none exist.  
• If R1 is not a partial order, provide a clear and concise explanation why not.  


2. Consider the relation R2 = {(7, 7), (7, 8), (8, 8), (8, 9), (9, 9), (9, 8), (0, 0)}, defined on the set  A2 = {7, 8, 9, 0}.  
Determine whether R2 is a partial order on A2 and support your answer as follows:  

• If R2 is a partial order:  
– Give all minimal elements of the poset (A2, R2) or explain why none exist.  
– Give all maximal elements of the poset (A2, R2) or explain why none exist.  
• If R2 is not a partial order, provide a clear and concise explanation why not.  

3. Consider the relation R3 = {(1, 1), (2, 2), (3, 2), (3, 3)} ∪ {(x, y) ∈ Z+ × Z+ : x > 3 and x ≤ y},  defined on the set A3 = Z+.  
Determine whether R3 is a partial order on A3 and support your answer as follows:  

• If R3 is a partial order:  
– Give all minimal elements of the poset (A3, R3) or explain why none exist.  
– Give all maximal elements of the poset (A3, R3) or explain why none exist.  
• If R3 is not a partial order, provide a clear and concise explanation why not.  

4. Consider the set ABCs, which is defined recursively as follows:  
• The string ca is in ABCs.  
• The string acab is in ABCs.  
• If strings s and t are in ABCs, then string bsbta is also in ABCs.  
To be explicit, each element of ABCs is some combination of characters a, b, and c.  
We can define recursive functions numA and numB that calculate the number of a’s (and b’s, respectively) in a given string:  
numA(ca) = 1 numB(ca) = 0  
numA(acab) = 2 numB(acab) = 1  
numA(bsbta) = 1 + numA(s) + numA(t) numB(bsbta) = 2 + numB(s) + numB(t)  
Your task: Use structural induction to prove the following claim:  
For all $s ∈ ABCs, numA(s) > numB(s)$. (That is, every element of ABCs contains  
more a’s than b’s.)  

### Basis


5. As discussed in lecture, the set FBT of full binary trees can be defined recursively as follows:  
• A single node is a full binary tree.  
• If T1 and T2 are both full binary trees, then $T1 \bowtie T2$ is a full binary tree.  
Recall: The notation $T1 \bowtie T2$ denotes the tree obtained by creating a new root node, with T1 as its left subtree and T2 as its right subtree.  

The number of edges and of nodes of a binary tree T can be calculated using the functions  edges(T) and nodes(T), defined as follows:  
• If T is a single node, then edges(T)  = 0 and nodes(T) = 1.  
• If T is a tree $T1 \bowtie T2$, then  
$edges(T1 \bowtie T2) = 2 + edges(T1) + edges(T2)$ $nodes(T1 \bowtie T2) = 1 + nodes(T1) + nodes(T2)$
Your task: Use structural induction to prove the following claim:  
For every full binary tree T , edges(T) = nodes(T ) − 1.  