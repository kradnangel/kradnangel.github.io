---
layout: post
title: Data Structure Summary
categories: [DataStructure]
tags: [DataStructure]
fullview: true
---
## Tree

### Rank
Rank is the number of nodes in the Left sub tree plus one.

For binary search tree, the rank of node equals to the order of node. (Q: [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) follow up)

### Binary tree

* a tree data structure
* each node has at most two children

#### Binary Search Tree(BST)

#### ALV Tree(self-balancing binary search tree)

* Search, insert, delete: O(log n) on average and worst case

#### Segment tree

* For storing intervals, or segments
* its structure cannot be modified once it is built.



## Graph

* an abstract data type
* undirected graph / directed graph
* Representations: Adjacency list / Adjacency matrix

### Outline
![](/images/Graph.png)

### Directed graph
* the edges have a direction
* simple graph (A directed graph is called a simple graph if it has no multiple arrows and no loops.)

#### Degree
Indegree: For a vertex, the number of tail ends adjacent to a vertex is called the indegree of the vertex.

Outdegree: For a vertex, the number of head ends adjacent to a vertex is its outdegree.

#### Connectivity
Weakly connected: if the undirected underlying graph obtained by replacing all directed edges of the graph with undirected edges is a connected graph.

Strongly connected: if it contains a directed path from x to y and a directed path from y to x for every pair of vertices {x, y}.

### Graph traversal

#### Path

Longest path in undirected acycle graph:

1. randomly pick up a node 'u' and BFS to find the farthermost node 'v' to 'u'. 
2. From 'v', find its farthermost node 'w'.
3. The longest path is the path from 'v' to 'w'


## Heaps

### Binary heap

####Basic

* A heap data structure
* using a binary heap to construct
* Shape property -- complete binary tree
* Heap property -- All nodes are either greater than or equal to (or less than or equal to) each of its children

### Complexity 

| |Average	|Worst case|
|-|-|-|
|Space	|O(n)	|O(n)|
|Search	|O(n)	|O(n)
|Insert	|O(1) 	|O(log n)
|Delete	|O(log n)|	O(log n)
|Peek	|O(1)	|O(1)

##Priority queue

###Basic

* A abstract data type
* = regular queue/stack + each element with priority
* Service order
	* (Different priority) element with high priority > element with low priority
	* (Same priority) accoding to element's order in the queue.
	
	
### Implement -- heaps

(In python -- binary min-heap -- 'heapq')
Take binary min-heap as an example

####Insert

1. Add the element to the end of heap
2. 'bubble-up'. Swap with its father till it's larger or equal to its father.

####Return min element

1. return root

####Return and Delete the min element

1. return root
2. replace the root with the last element in heap
3. 'bubble-down'. swap with its smaller children till it's smaller than all of its children

### Complexity 

Same as binary heap