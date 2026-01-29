202503041211
Status: #idea
Tags:[[List (Java)]]

A singly-linked list is a data structure for implementing a list ADT, where each node has data and a pointer to the next node.

## Common Methods:

### Append:
```java
ListAppend(list, item) {
   newNode = Allocate new singly-linked list node
   newNode⇢data = item
   newNode⇢next = null
   ListAppendNode(list, newNode)
}

ListAppendNode(list, newNode) {
   if (list⇢head == null) { // List empty
      list⇢head = newNode
      list⇢tail = newNode
   }
   else {
      list⇢tail⇢next = newNode
      list⇢tail = newNode
   }
}
```

### Prepend:
```java
ListPrepend(list, item) {
   newNode = Allocate new node with item as data
   ListPrependNode(list, newNode)
}

ListPrependNode(list, newNode) {
   if (list⇢head == null) {
      list⇢head = newNode
      list⇢tail = newNode
   }
   else {
      newNode⇢next = list⇢head
      list⇢head = newNode
   }
}
```

### Search
```java
ListSearch(list, key) {
   curNode = list⇢head
   while (curNode is not null) {
      if (curNode⇢data == key) {
         return curNode
      }
      curNode = curNode⇢next
   }
   return null
}
```
Worst Case: O(N)
### Insert:
```Java
ListSearch(list, key) {
   curNode = list⇢head
   while (curNode is not null) {
      if (curNode⇢data == key) {
         return curNode
      }
      curNode = curNode⇢next
   }
   return null
}
```
Worst Case: O(N)
### Insert Node After:
```Java
ListInsertNodeAfter(list, currentNode, newNode) {
   // Special case for empty list
   if (list⇢head == null) {
      list⇢head = newNode
      list⇢tail = newNode
   }
   else if (currentNode == list⇢tail) {
      list⇢tail⇢next = newNode
      list⇢tail = newNode
   }
   else {
      newNode⇢next = currentNode⇢next
      currentNode⇢next = newNode
   }
}
```
Worst Case: O(1)
### Insert Item After:
```java
ListInsertAfter(list, currentItem, newItem) {
   currentNode = ListSearch(list, currentItem)
   if (currentNode != null) {
      newNode = Allocate new singly-linked list node
      newNode⇢data = newItem
      newNode⇢next = null
      ListInsertNodeAfter(list, currentNode, newNode)
      return true
   }
   return false
}
```
Worst Case: O(N)

### Remove:
```Java
ListRemove(list, itemToRemove) {
   // Traverse to the node with data equal to itemToRemove, 
   // keeping track of the previous node in the process
   previous = null
   current = list⇢head
   while (current != null) {
      if (current⇢data == itemToRemove) {
         ListRemoveNodeAfter(list, previous)
         return true
      }
         
      // Advance to next node
      previous = current
      current = current⇢next
   }
      
   // Not found
   return false
}
```
Worst Case: O(N)