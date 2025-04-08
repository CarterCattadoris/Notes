
stack = LIFO
	stack "peek" returns top element
	push adds, pop removes
Queue = FIFO
	offer adds element
	poll removes
	peek returns front element
circular queue
	for full, rear = capacity - 1 and front = 0, and front = (rear+1) % capacity
	for empty, front = rear = -1, and front = (rear+1) % capacity
big O
	i /= 2 means log n for loops
	common: O(1), O(log n), O(n), O(n log n), O(n^2), O(2^n), O(n!)
Linked List
	**with head pointer only**
	O(1):
		add and remove from front of the list
	**with head and tail pointers**
	O(1):
		add and remove to the front of the list, add to the end of the list
	O(n):
		remove and element in the middle index
	**double linked list with tail pointer only**
	O(1):
		add and remove to the end of the list
	**singly linked circular list with head pointer**
	O(1):
		add and remove to front/end of the list
	**Add an element to a sorted doubly linked list in the correct position**
		O(n)
	**Sort a singly linked list with only head pointer**
		Depends on sorting alg, bubble sort = O(n^2), merge sort O(n log n)
	**Sort a singly linked list with both head and tail pointers**
		same as previous
Postfix
	"126 8 - 7 24 + * 3 / 20 24 + +". 
	Answer:
	126 8 - 7 24 + * 3 / 20 24 + +
	118 7 24 + * 3 / 20 24 + +
	118 31 * 3 / 20 24 + +
	3,658 3 / 20 24 + +
	1,219 20 24 + +
	1,219 44 +
	1,263



study sheet

1) 10,80,70,70
2) 10,20,40, 70
	1) 30 20 40 70
	2) 10, 20, 40, 70
3) circular queue length 6
	1) front = 0, rear = 0
	2) front = 0, rear = 1
	3) front = 0, rear = 2
	4) front = 1, rear = 2
	5) front = 1, rear = 3
	6) front = 2, rear = 3
	7) front = 3, rear = 3
	8) front = 4, rear = 3
4) for full, rear = capacity - 1 and front = 0, and front = (rear+1) % capacity
5) x
6)  x
7) G -> F -> A -> B -> E -> C
8) x
9) method returns the length of the list, but deletes all the elements (head = head.next), also wouldnt work on an empty list
10) x
	1) C
	2) A
	3) C
	4) C
	5) A
	6) D (var2)
	7) null
	8) null
11) x
	1) O(n^2)
	2) O(n log n)
12) inverts the string