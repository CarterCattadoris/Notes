
Stack - LIFO

Queue - FIFO

Java interface 
	no constructor needed
	class implementing needs to implement all methods

Abstract class 
	cannot directly instantiate a class, need to implement methods

Hash table
	Effecting efficiency
		ratio of elements stored to number of buckets
		number of keys in each bucket
		how it handles collisions
Cryptographic hash function
	Same input gives same output
	Collision free (hash(x) != hash(y) given x !=y)
	cant find input based off hash output

Sorts tested with {4, 11, 2, 7, 8, 1}
Insertion sort
	O(n^2) unless sorted which is O(n)
	
bubble sort
	O(n^2)
	4 vs 11 OK, 11 vs 2 swap, 11 vs 8 swap, 11 vs 1 swap{4,2,7,8,1,11}
	4 vs 2 swap, 4 vs 7 ok, 7 vs 8 ok, 8 vs 1 swap{2,4,7,1,8,11}
	2 vs 4 ok, 4 vs 7 ok, 7 vs 1 swap {2,4,1,7,8,11}
	2 vs 4 ok, 4 vs 1 swap
	2 vs 1 swap
selection sort
O(n^2)
merge sort
O(n log n)
quick sort
O(n^2) with bad pivots, else O(n log n)