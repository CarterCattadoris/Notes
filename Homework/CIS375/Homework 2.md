I discussed Problems 2 and 3 with Rio Harper at a conceptual level.

## Proof 1
Definition: An integer p is a perfect square provided there is an integer i such that p = i^2.
### Claim: 
Let m and n be integers. If m and n are both perfect squares, then their product mn is also a perfect square.
#### Proof:
1. Proof: (Direct)
	1. Suppose that m and n are integers and perfect squares
	2. NTS: mn is a perfect square, which means that $mn = i^2$ 
	3. Because m and n are perfect squares, there exists integer x and y such that $m=x^2, n=y^2$ 
	4. By algebra, $mn = x^2 \cdot y^2 = (xy)^2$ 
	5. Because x and y are integers, so is $(xy)$ 
	6. Hence, there is an integer i(i.e, $(xy)$) such that $mn = i^2$ 
	7. Therefore mn is a perfect square

## Proof 2
Definition: Let x and y be integers. We says that x tempers y provided that there is an integer k such that $2x + 7y = 3k$.
### Claim: 
Let a, b, c be integers. If a tempers b and b tempers c, then a tempers c.
#### Proof
2. Proof: (Direct)
	1. Suppose that a,b,c are integers and a tempers b and b tempers c
	2. NTS: a tempers c, which means that $2a + 7c = 3k$ provided integers $a,b,c,$ and $k$
	3. Because a tempers b and b tempers c, there exists integers $a,b,c,k_1$ and $k_2$ such that $2a+7b=3k_{1},2b+7c=3k_2$
	4. By algebra, $$2a + 7b+2b+7c = 3k_1+3k_2$$$$2a+7c+9b=3k_{1}+3k_{2}$$$$2a+7c=3k_{1}+3k_{2}-9b$$$$2a+7c=3(k_{1}+k_{2}-3b)$$
	8. Since $k_{1},k_{2},b$ are all integers, so is $(k_{1}+k_{2}-3b)$
	9. Thus, there exists an integer k (i.e $(k_{1}+k_{2}-3b)$) such that $2a+7c=3k$ 
	10. Therefore, a tempers c

## Proof 3
Definition: An integer n is sonic provided that $6|(n^2 + 4n)$.
### Claim: 
Let q be an integer. If 3|q, then 2q is sonic
#### Proof:
1. Proof:(Direct)
	1. Suppose that q is an integer and 3|q
	2. NTS: $6|(2q)^2+4(2q)$, which means there is an integer p such that $6p=(2q)^2+4(2q)$ 
	3. Since 3|q, that means there is an integer k such that 3k = q
	4. By algebra, 2q = 6k
	5. Substituting this into the definition for a sonic integer(as $n=2q=6k$), we get $(2q)^2+4(2q)=(6k)^2+4(6k)=36k^2+24k=6(6k^2+4k)$ by algebra
	6. Because k is an integer, there exists an integer p(i.e $k^2+4k$) such that $6p=(2q)^2+4(2q)$
	7. Thus, $6|(2q)^2+4(2q)$ 
	8. Therefore, 2q is sonic