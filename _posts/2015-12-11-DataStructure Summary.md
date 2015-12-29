---
layout: post
title: Data Structure Summary
categories: [DataStructure]
tags: [DataStructure]
fullview: true
---
AVL Tree / 平衡二叉树
	- 查找、插入和删除在平均和最坏情况下都是O（log n）
	- 增加和删除可能需要通过一次或多次树旋转来重新平衡这个树。




寻找树形图中的最长路径
Question:
在一个迷宫中找距离最长的两个点。
 
迷宫可以看作是一个无根树，因此，这个问题等价与在一个树形图中找最远的两个节点，也叫做这个图的直径。迷宫、树形图有个很好的特点：即任意两个节点之间的距离就是这两点之间的最短路径和最长路径，也可以说任意两个节点之间的距离一定的。

Algorithm:
任选一点u为起点，对树进行BFS遍历，找出离u最远的点v。然后以v为起点，再进行BFS遍历，找出离v最远的点w。则v到w的路径长度即为树的直径。时间复杂度为O(n)。


## Tree

### Rank
Rank is the number of nodes in the Left sub tree plus one.

For binary search tree, the rank of node equals to the order of node. (Q: [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) follow up)

### Binary tree

* a tree data structure
* each node has at most two children


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