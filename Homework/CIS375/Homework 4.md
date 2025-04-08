I received no assistance on this assignment
## Proof 1
Claim: Let W,X,Y be sets. If $W \subseteq X \cap Y,\space then \space W \subseteq Y$
Proof:(direct)
- Suppose $W\subseteq X\cap Y$
- (NTS: $W \subseteq Y$)
- Consider an arbitrary element $z \in W$ 
- Since $z \in W$ and $W \subseteq X \cap Y$, $z \in X\cap Y$
- By definition of intersection, $z\in X,and\space z \in Y$ 
- Because z was an arbitrary element of W, $W \subseteq Y$ 
## Proof 2
Claim: Let F,G,H be sets. Then $(F \cap G) - H \subseteq(F-H)\cap(G-H)$ 
Proof:(direct)
- Consider an arbitrary element $w \in (F \cap G)-H$ 
- (NTS: $w \in (F-H) \cap (G-H)$ 
- By definition of set difference, $w \in (F\cap G)$ and $w \notin H$ 
- By definition of intersection, $w \in F$ and $w \in G$ 
- Because $w \in F$ and $w \not\in H$, $w \in (F-H)$
- Because $w \in G$ and $w \not\in H$, $w \in (G-H)$ 
- Because $w \in (F-H)\space and\space w \in(G-H)$, $w \in (F-H)\cap(G-H)$
- Because w was an arbitrary element of $(F \cap G)-H$, $(F\cap G)-H \subseteq (F-H)\cap (G-H)$

## Proof 3
Claim: Let Q and R be sets. Then $2^{Q\cap R} \subseteq 2^Q \cap 2^R$ 
Proof:(direct)
- Consider an arbitrary element $w \in 2^{Q\cap R}$ 
- (NTS: $w \in 2^Q\cap2^R$)
- By definition of powerset, $w \subseteq Q \cap R$
- By definition of intersection, $w \subseteq Q$ and $w \subseteq R$ 
- Therefore, $w \in 2^Q$ and $w \in 2^R$
- Thus by definition of intersection,  $w \in 2^Q \cap 2^R$
- Since w was an arbitrary element of $2^{Q\cap R}$, $2^{Q\cap R} \subseteq 2^Q \cap 2^R$  

## Proof 4:
Claim: Let A,B,C,D be sets. Then $(A-B) \times(C-D)\subseteq(A \times C) - (B \times D)$
Proof:(direct)
- Consider an arbitrary element $(e,f) \in (A-B) \times (C-D)$
- (NTS: $w \in (A \times C) - (B \times D)$)
- Because $e \in (A-B)$, we know $e \in A$ and $e \not\in B$ 
- Because $f \in (C-D)$, we know $f \in C$ and $f \not\in D$
	- Since $e \in A$ and $f \in C$, $(e,f) \in (A\times B)$ 
	- Since $e \not\in B$ and $f \not\in D$, $(e,f) \not\in (B\times D)$ 
- Therefore, $(e,f) \in (A\times C)-(B\times D)$ 
- Since (e,f) was an arbitrary element of $(A-B) \times (C-D)$, $(A-B) \times(C-D)\subseteq(A \times C) - (B \times D)$ 