202503251123
Status: #idea
Tags:[[Discrete Math (CIS375)]], [[Proofs]]

**Mathematical induction** is a [[Proofs|proof technique]] for establishing statements about all natural numbers or integers above a base case.

Proof: By mathematical induction  
- Let $P (n)$ be the statement: **#1  
- Basis: P(**#2**) is true, because **#3 
- Inductive step: Suppose k ≥ **#2** . For the inductive hypothesis, suppose P(k) is true: **#4**  
- We need to show that P(k+1) is true: **#5 
- **Heart of the inductive step: show that P(k + 1) is true whenever P(k) is**
- Thus, for all k ≥ **#2** , the conditional $P (k) → P (k + 1)$ is true.  
- By the basis, inductive step, and the principle of mathematical induction(pmi), the claim is true.  

How to fill in the various blanks:  
**#1**: Write the general form of what you’re trying to prove for each value n  
- Remember: in effect, you are defining P to be a macro that (when given a specific value v) expands into a statement about v; you are not claiming the veracity of said statement. 
**#2**: Fill in the least integer m for which you want to prove P(m).  
- For example, to prove that the property holds for all integers greater than or equal to 7, you fill in the number 7.  
**#3**: Include the work necessary to demonstrate that the basis holds.  
**#4**: Expand out the statement P(k).  
**#5**: Expand out the statement P(k + 1).  

## Examples:

### Example 1:

Claim: for every natural number m, $11^m - 4^m$ is divisible by 7

Proof: by mathematical induction
- Let P(n) be the statement: $11^m-4^m$ is divisible by 7
- Basis: P(0) is true, because $11^0 - 4^0=1-1=0$, which is divisible by 7
- Inductive Step: Suppose $k \geq 0$. For the inductive hypothesis, Suppose that the statement P(k) is true: $11^k-4^k$ is divisible by 7
- NTS: $P(k+1)$ is true: $11^{k+1} - 4^{k+1}$ is divisible by 7
- By algebra we see that: $11^{k+1}-4^{k+1}=11\cdot 11^k-4\cdot 4^{k}=(7+4)11^k-4\cdot 4^k=7\cdot 11^k+4(11^k-4^k)$ 
- By the inductive hypothesis(IH), $11^k-4^k$ is divisible by 7, so $4\cdot (11^K-4^k$ is divisible by 7 and $7\cdot 11^k$ is divisible by 7, so the sum $7\cdot 11^k+4(11^k-4^k)$ is divisible by 7
- Thus, for all $k \geq 0$, the conditional $P(k) \to P(k+1)$ is true
- By the basis, the inductive step, and the PMI, the claim is true

## Related Proof Techniques
- [[Direct Proofs]]
- [[Proof by Contraposition]]
- [[Proof by Contradiction]]
- [[Structural Induction]]

---
### References
- [[Discrete Math (CIS375)]]