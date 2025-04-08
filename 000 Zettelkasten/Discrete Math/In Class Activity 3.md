202502041159
Status: #idea
Tags:[[Sets]]

Consider the following sets of animals:
B : the set of animals that burrow
F : the set of animals that are furry
G : the set of animals that growl
H : the set of animals that hibernate
N : the set of animals that are nocturnal
T : the set of animals with big teeth
1. Express each of the following English statements using the language of set theory:
	(a) Every nocturnal animal either has big teeth or growls (or both).
	$N \subseteq T \cup G$
	(b) There are some burrowing animals that hibernate but are not nocturnal.
	$B \cap H \nsubseteq N$, $(B \cap H) - N \neq \emptyset$
	(c) There are no animals that both burrow and hibernate.
	$B \cap H = \emptyset$
	(d) There are fewer animals that hibernate than there are furry animals that growl.
	$|H| \leq |F \cap G|$

2. Express each of the following statements in everyday (but unambiguous) English:
	(a) $G ⊆ T ∪ H$
	Every animals that growls either has big teeth or hibernate (or both)
	(b) $(F \triangle B) \nsubseteq T$
	At least one animal that is furry or burrows (but not both) doesn't have big teeth
	(c) $(N − G) = F ∩ H$
	Every animal that is nocturnal that doesn't growl are exactly the animals that are furry and hibernate