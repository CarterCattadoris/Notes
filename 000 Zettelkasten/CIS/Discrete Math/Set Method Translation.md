202502041152
Status: #idea
Tags:[[Sets]]

C : set of people who are Canadians
F : set of people who speak French
M : set of people who are in the military
E : set of people who are engineers

- $C ∩ M$
	- Set of Canadians who are in the military
- $E − F$
	- Set of engineers who don’t speak French
- $M \triangle E$
	- Set of people who are in the military or are engineers (but not both)
- $F ∩ E 6 = ∅$ 
	- “There is at least one French-speaking engineer.”  
	- “Some engineers speak French.”  
- $C ⊆ M ∪ F$
	- “Every Canadian is either in the military or speaks French (or both).

- Jane is a French speaking Canadian engineer
	- $Jane \in F \cap C \cap E$
- All Canadian engineers who are in the military speak french
	- $C \cap E \cap M \subseteq F$ 
- No one in the military speaks French
	- $M \cap F = \emptyset$ or $M-F=M$
- There is at least one Canadian who does not speak French
	- $C - F \neq \emptyset$ or $C \nsubseteq F$ 