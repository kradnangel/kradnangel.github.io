---
layout: post
title: Data Structure Summary
categories: [DataStructure]
tags: [DataStructure]
fullview: true
---

### Tree

#### Binary tree

* a tree data structure
* each node has at most two children

### Heaps

#### Binary heap

#####Basic

* A heap data structure
* using a binary heap to construct
* Shape property -- complete binary tree
* Heap property -- All nodes are either greater than or equal to (or less than or equal to) each of its children

#### Complexity 

| |Average	|Worst case|
|-|-|-|
|Space	|O(n)	|O(n)|
|Search	|O(n)	|O(n)
|Insert	|O(1) 	|O(log n)
|Delete	|O(log n)|	O(log n)
|Peek	|O(1)	|O(1)

###Priority queue

####Basic

* A abstract data type
* = regular queue/stack + each element with priority
* Service order
	* (Different priority) element with high priority > element with low priority
	* (Same priority) accoding to element's order in the queue.
	
	
#### Implement -- heaps

(In python -- binary min-heap -- 'heapq')
Take binary min-heap as an example

#####Insert

1. Add the element to the end of heap
2. 'bubble-up'. Swap with its father till it's larger or equal to its father.

#####Return min element

1. return root

#####Return and Delete the min element

1. return root
2. replace the root with the last element in heap
3. 'bubble-down'. swap with its smaller children till it's smaller than all of its children

#### Complexity 

Same as binary heap
	