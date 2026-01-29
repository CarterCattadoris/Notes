202501231504
Status: #idea
Tags:[[Logic]], [[Discrete Math (CIS375)]], [[Proofs]]


---
### References
To show the statement is false: 
Give (and show) a ***specific case*** that makes A true and B false. This specific case serves as a [[Counterexample]]

Claim: if x and y are integers such that $x|y$, then $x \leq y$
Claim is false: Let $x = 2$ and y = −6. Then 2| − 6 (because 2 · −3 = −6),
but it is not the case that 2 ≤ −6.

Show that, whenever A is true, B is also true

In a direct proof we suppose A is true and find B

## Formatting:
[[Proof Formatting]]

### Example 1:
#### Claim: 
If x and y are even integers, then $x + y$ is even

##### Proof: 
(Direct)

Suppose x and y are even integers

Because x and y are even, there exists integers a and b such that:	

$$
x = 2a, y = 2b 
$$
By algebra, 
$$
x+y=2a+2b=2(a+b) 
$$

Because a and b are integers, so is $a+b$

Thus, there is an integer k (i.e $a+b$) such that $x+y=2k$ 

Thus, $x+y$ is even


###### Scratch Work:
- What we know:
	- x is an even integer
	- y is an even integer
	- [[Proof Facts]]
	-  $\exists$ integers a,b such that x = 2a, y = 2b
		- $x + y = 2a + 2b$
		- $x+y=2(a+b)$

- What we need:
	- $x + y$ is even
	- $\exists$ integer k such that $x+y = 2k$ 

# Example 2:
## Claim: 
Let a,b,c be integers, if $a|b$ and $b|c$, then $a|c$

### Proof:
(Direct)

Suppose $a|b$ and $b|c$ 

(NTS: $a|c$, which means that there is some integer d such that $a\cdot d = c$)

Because $a|b$ and $b|c$, there are integers f and n such that $a \cdot f = b$ and $b \cdot n =c$ 

By algebra, $c = b \cdot n = (a \cdot f) \cdot n = a \cdot (f \cdot n)$ 

Because f and n are integers, so is $f \cdot n$ 

Thus, there is an integer d (namely $f \cdot n$) such that $a \cdot d =c$ 

Thus, $a | c$ 

#### Scratch Work:
- What we know:
	- [[Proof Facts]]
	- $a|b$
		- $\exists$ integer f such that $a \cdot f = b$ 
	- $b|c$
		- $\exists$ integer n such that $b \cdot n=c$
	- $c = b \cdot n$
	- $c = (a \cdot f) \cdot n = a \cdot (f \cdot n)$  -> plugging in $a \cdot f$ for b

- What we need
	- $a|c$
		- $\exists$ integer d such that $a\cdot d=c$

## Related Proof Techniques
- [[Proof by Contraposition]]
- [[Proof by Contradiction]]
- [[Mathematical Induction]]

---
### References
- [[Discrete Math (CIS375)]]