
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
	start with {4}
	insert 11, insert 2 shift 4 and 11
	insert 7 shift 11
	insert 8 shift 11
	insert 1 shift all
bubble sort
	O(n^2)
	4 vs 11 OK, 11 vs 2 swap, 11 vs 8 swap, 11 vs 1 swap{4,2,7,8,1,11}
	4 vs 2 swap, 4 vs 7 ok, 7 vs 8 ok, 8 vs 1 swap{2,4,7,1,8,11}
	2 vs 4 ok, 4 vs 7 ok, 7 vs 1 swap {2,4,1,7,8,11}
	2 vs 4 ok, 4 vs 1 swap
	2 vs 1 swap
selection sort
	O(n^2)
	find min, insert at ith place in array
merge sort
	O(n log n)
	split array until left with single element arrays, merge pairs until array is built
quick sort
	O(n^2) with bad pivots, else O(n log n)
	pivot = 4, left {2,1}, right {11,7,8}
	Left {2,1}
	Pivot 2, left {1} right {} -> sorted {1,2}
	Right {11,7,8}
	pivot 11
	left{7,8}, right {} -> recurse on {7,8}
	sub-right{7,8}
	pivot = 7, left{}, right{8} -> sorted {7,8}
	put together	
Tree Traversal
	In order
		Left -> Root  -> right
	Pre order
		Root -> left -> right
	Post Order
		Left right root
	Breadth first
		level by level, top down
		queue
	depth first
		go all the way down left, then go back and start on right
		stack
Min Heap
	each parent is <= its child node
	all levels must be filled left to right to start new level

T,h,e, ,d,o,r,s,l,a,m
1 1 2 2 2 2 1 1 1 1 2 
  x     x 
T h  r  s
 2xe, 2xo, 2xm
T 0000
h 0001
e 0010
space 0011
d 0100
o 0101
r 0110
s 0111
l 1000
a 1001
m 1010

