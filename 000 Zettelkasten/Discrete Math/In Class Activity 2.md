202501281121
Status: #idea
Tags:[[Direct Proofs]]

## Claim: 
Let n be an integer. If n is even, then $4 | n^2$	
### Proof:
1. Proof: (Direct)
	1. Suppose n is even
	2. NTS: $4|n^2$, which means that there is an integer c such that $4 \cdot c = n^2$
	3. Because n is even, there is an integer k such that $n = 2k$ 
	4. By algebra, $n^2=(2k)^2=4k^2$
	5. Because k is an integer, so is $k^2$
	6. Therefore, there is an integer c(namely $k^2$) such that $4c = n^2$ 
	7. Thus, $4 | n^2$.

#### Scratch: 
1. We have
	1. n is even
		1. $\exists$ k such that $n = 2k$ 
		2. $n^2 = (2k)^2 = 4k^2$ and $k^2$ is an integer  

1. We want
	1. $4|n^2, \exists$ c such that $4\cdot c = n^2$ 


# Proof 2:

## Claim: 
let m and p be integers. If m and p are both odd, then their product $m \cdot p$ is odd

### Proof: 
1. Proof:(Direct)
	1. Suppose that m and p are both odd
	2. NTS: $mp$ is odd which means that $mp = 2k + 1$ 
	3. Because m and p are odd, there are integers a and b such that $m = 2a + 1$ and $p = 2b + 1$ 
	4. By algebra, $mp = (2a+1) \cdot (2b+1)=4ab+2a+2b+1=2(2ab+a+b) + 1$  
	5. Because a and b are integers, so is $(2ab + a + b)$ 
	6. Hence, there is an integer k(i.e, $2ab + a + b$) such that $mp = 2k + 1$ 
	7. Therefore, mp is odd
#### Scratch: 
1. We have:
	1. m and p are odd
		1. $\exists$ integers j and k such that $m = 2j + 1$ and $p = 2k + 1$
		2. $mp = 4jk + 2j + 2k + 1$ 

1. We want: 
	1. $m \cdot p$ is odd

# Proof 3:
Definitions:
An integer n is cordial provided tat there is an integer k such that $n=6k+1$ 
An integer is glib provided that there is an integer k such that $n=5k-1$ 

## Claim: 
Let c and g be integers. if c is cordial and g is glib, then 5c + 6g is glib

### Proof: 
1. Proof:(direct)
	1. Suppose c is cordial and g is glib
	2. NTS: 5c + 6g is glib which means there is an integer k such that 5c + 6g = 5k-1
	3. Because c is cordial and g is glib, there exists integers n and b such that $c=6n+1,g=5b-1$ 
	4. By algebra, $5c+6g =5(6n+1)+6(5b-1)=30n+5+30b-6=30n+30b-1=5(6n+6b)-1$
	5. Because n and b are integers, so is $6n+6b$ 
	6. Thus, there exists an integer k such that $5c+6g = 5k-1$
	7. Thus, 5c+6g is glib



---
### References
