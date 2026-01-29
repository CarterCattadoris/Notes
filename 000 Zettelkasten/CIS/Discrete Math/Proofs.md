202501231459
Status: #MOC
Tags:[[Logic]], [[Discrete Math (CIS375)]]

A **proof** is an argument from hypotheses (assumptions) to a conclusion.

## Examples:

### Example 1:
Suppose we wish to show that $H_{1} \land H_{2} \land \dots \land H_{k} \implies C$

| Method of Proof             | What to Suppose                                | What to Show                           |
| --------------------------- | ---------------------------------------------- | -------------------------------------- |
| [[Direct Proofs]]           | $(H_{1} ∧ H_{2} ∧ · · · ∧ H_{k})$              | $C$                                    |
| [[Proof by Contraposition]] | $\neg C$                                       | $\neg (H_{1} ∧ H_{2} ∧ · · · ∧ H_{k})$ |
| [[Proof by Contradiction]]  | $(H_{1} ∧ H_{2} ∧ · · · ∧ H_{k}) \land \neg C$ | $A \space CONTRADICTION$               |

### Example 2:
Let m and n be integers. If the product mn is odd, then both m and n are odd.

| Method of Proof             | What to Suppose                                              | What to Show                     |
| --------------------------- | ------------------------------------------------------------ | -------------------------------- |
| [[Direct Proofs]]           | mn is odd                                                    | both m and n are odd             |
| [[Proof by Contraposition]] | It's not the case that both m and n are odd                  | It's not the case that mn is odd |
| [[Proof by Contradiction]]  | - mn is odd<br>- It's not the case that both m and n are odd | A contradiction                  |

### Example 3:
Consider the following claim:  
Let x, y, z be integers. If x is brazen and ($y ⊕ z$) is not claibic, then x filters $z^y$.  

Note: I am not asking you to prove this claim, so you do not need to worry about the  
definitions of brazen, claibic, ⊕, or filters.  

1. Suppose you decide to prove this claim via a direct proof.  
	1. What would you need to suppose? 
		1. x is brazen and ($y ⊕ z$) is not claibic
	2. What would you need to show?  
		1. x filters $z^y$
2. Suppose you wanted to prove this claim via a proof by contraposition.  
	1. What would you need to suppose?  
		1. x doesn't filter $z^y$
	2. What would you need to show?  
		1. either x is not brazen or ($y ⊕ z$) is claibic (or both)
3. Suppose you wanted to prove this claim via a proof by contradiction.  
	1. What would you need to suppose?
		1. x is brazen and ($y ⊕ z$) is not claibic and x doesn't filter $z^y$
	2. What would you need to show?
		1. A contradiction