202502061129
Status: #idea
Tags:[[Sets]], [[Proofs]]

## Existential Statements
To prove a statement of the form "There exists $x \in U$ such that P(x)"
- Give a specific value $v \in U$ 
- Show that P(v) is true

### Example: 
Claim: There is a set X such that $\{ 1,2 \} \nsubseteq X$ and $|2^X| > 10$ 
- Let $X = \{1, 2, 3, 4\}$. We can see that {1, 2} ⊆ X .
- Recall that, for any set Y , |2Y| = 2|Y|. Because |X| = 4, we can see that |2X| = 2|X| = 24 = 16 > 10. Therefore, the claim is true.

## Universal Statements
To prove a statement of the form “Every x ∈ U satisfies P(x)”:
- Consider an arbitrary (i.e., nonspecific) object a ∈ U.
- Show that P(a) is true.

### Example:

Proof: (direct)
- Consider an arbitrary p ∈ E . (Need to show: $p^2$ is even, which means there exists integer k such that $p^2 = 2k$.)
- Because p ∈ E , we know $p ∈ \mathbb{Z}$ and p is even, and hence there is an integer  such that p = 2L. It follows that $$p^2 = (2L)^2 = 4L^2 = 2 · (2L^2)$$
- Because L is an integer, so is $2L^2$. Thus, there is an integer k (namely $2L^2$) such that $p^2 = 2k$, and $p^2$ is even. Because p was arbitrary, the claim is true

## Proofs about Subsets

### Examples:

#### Example 1:
Show that $W \subseteq Z$ 

Claim: Let A and B be sets. Then $A \cap B \subseteq A \cup B$
Proof: (direct)
- Consider an arbitrary $w \in A \cap B$. (NTS: $w \in A \cup B$)
- By the definition of $A \cap B$, we know $w \in A$. Thus, by the definition of $\cup,\space w \in A \cup B$ 
- Because w was an arbitrary element of $A \cap B,\space A \cap B \subseteq A \cup B$ 

#### Example 2:
Proposition: Let A,B,C be sets. If $A \subseteq B$ and $B \subseteq C$, then $A \subseteq C$

Proof:(direct)
- Suppose $A \subseteq B,and,B \subseteq C$
- NTS: $A \subseteq C$
- Consider an arbitrary element $w \in A$ (NTS: $w \in C$)
- Because $w \in A$ and $A \subseteq B, \space w \in B$ as well
- Because $w \in B,\space and \space A \subseteq B,\space w \in C$ as well
- Because w was an arbitrary element of A, $A \subseteq C$ 

#### Example 3:
Claim: Let A,B,C be sets. Then $(A-C) \cap B \subseteq (B-C) \cap A$ 

Proof:(direct)
- Consider an arbitrary element $w \in (A-C) \cap B$ 
- NTS: $w \in (B-C) \cap A$ 
- By definition of $\cap$, $w \in A-C\space and \space w \in B$
- By definition of $A-C,\space w \in A \space and \space w \notin C$ 
- Because $w \in B \space and \space w \notin C,\space w \in B-C$ 
- Because $w \in A,\space w\in (B-C) \cap A$ 
- Because w was an arbitrary element of $(A-C) \cap B$, $(A-C) \cap B \subseteq (B-C) \cap A$ 
#### Example 4: 
Claim: Let A,B,C be sets. If $A \subseteq B$ and $C \subseteq B$, then $A \cup C \subseteq B$

Proof:(direct)
- Suppose $A \subseteq B$ and $C \subseteq B$
- NTS: $A \cup C \subseteq B$
- Consider arbitrary $w \in A \cup C$
- By definition of $A \cup C$, at least one of the following cases is true:
	- $w \in A$: Because $A \subseteq B,\space w\in B$ as well
	- $w \in C$: Because $C \subseteq B,\space w\in B$
- Note that, in both cases, $w \in B$ 

#### Example 5:
Claim: Let A,B,C,D be sets. If $A \subseteq B\space and\space C \subseteq D,then\space A\times C \subseteq B \times D$ 

Proof:(direct)
- Suppose $A \subseteq B$ and $C \subseteq D$
- (NTS: $A \times C \subseteq B\times D$)
- Consider an arbitrary $y \in A\times C$
---
- By definition of $A \times C$, there are (specific) elements $a\in A$ and $c\in C$ such that $y=(a,c)$ (need $a \in B,\space c\in D$ to fit $y \in B\times D$)
- Because $a\in A$ and $A \subseteq B$, $a\in B$
- Likewise, because $c\in C$ and $C\subseteq D$, $c\in D$
- ##### **Can also write this as:**
- Consider an arbitrary $(a,c) \in A\times C$
---
- Because $a\in B$ and $c\in D$, we know $(a,c)\in B\times D$
- Because y was an arbitrary element of $A\times C$ and $y\in B\times D$, $A\times C \subseteq B\times D$

#### Example 6:
Claim: Let C and D be sets. if $C \subseteq D,$ then $2^C \subseteq 2^D$ 
Proof:(direct)
- Suppose that $C \in D$
- (NTS:$2^C \subseteq 2^D$)
- Consider an arbitrary $w \in 2^C$ 
- By definition of powerset, $w \subseteq C$ 
- Because $w \subseteq C$ and $C \subseteq D$, by subset transitivity, $w \subseteq D$ 
- Therefore, $w \in 2^D$. Because w was an arbitrary element of $2^C$, $2^C \subseteq 2^D$ 

#### Example 7:
Claim: Let C and D be sets. if $2^C \subseteq 2^D$, then $C \subseteq D,$ 

Proof:(direct)
- Suppose 