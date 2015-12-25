---
layout: post
title: LeetCode_310_Minimum Height Trees
categories: [LeetCode]
tags: [LeetCode, python, tree, Graph]
fullview: true
---
###[Question](https://leetcode.com/problems/minimum-height-trees/)

For a undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

Format

The graph contains n nodes which are labeled from 0 to n - 1. You will be given the number n and a list of undirected edges (each edge is a pair of labels).

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

Example 1:

Given n = 4, edges = [[1, 0], [1, 2], [1, 3]]

        0
        |
        1
       / \
      2   3
      
return [1]

Example 2:

Given n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

     0  1  2
      \ | /
        3
        |
        4
        |
        5
        
return [3, 4]
	
### Solution

First of all, this question is asking us to make a node as the root to make the tree has the minimum height. So, the simplest idea to solve this question is trying to make every node as the root, then check the height of the tree. However, the time complexity is O(n^2).

Therefore, let's think about the shape of the minimum height tree. We can notice that the difference of the height of highest subtree and the height of second-highest subtree shoule be 0 or 1. If the difference is larger than 1, we can reduce the height of the whole tree by taking the root of highest subtree as the root of the whole tree. So, in this case, we should also notice that, the path from the leaf of highest subtree to the leaf of the second-highest subtree should be the longest path in this undirected graph. So, the root should locate in the midpoint of this path. If the length of path is even, there is two possible roots. If the length of path is odd, the midpoint of this path is the only node which could be chosen as the root. So, this question has been translated as finding the longest path in the graph.

The algorithmt used to find the longest path is that:

1. randomly pick up a node 'u' which has 1 degree.
2. BFS to find the farthest node 'v' to this node.
3. From node 'v', BFS to find the farthest node 'w' to it.
4. The path from 'v' to 'w' is the longest path in this graph

The time complexity is O(n).

Other simple but useful solution to this question is deleting leaves (all the node with 1 degree) iteratively until these is only one or two node left. This(These) node(s) is(are) the root(s) which will lead to a minimum height tree.

The time complexity could be O(n).

### Code
	class Solution(object):
	    def findMinHeightTrees(self, n, edges):
	        """
	        :type n: int
	        :type edges: List[List[int]]
	        :rtype: List[int]
	        """
	        if n == 1:
	            return [0]
	        elif n == 2:
	            return [0,1]
	
	        from collections import defaultdict
	        e = defaultdict(list)
	        for v,w in edges:
	            e[v].append(w)
	            e[w].append(v)
	        
	        u = 0
	        def longPath(p):
	            stack = list(e[p])
	            path = [p]
	            longest = []
	            while stack:
	                p = stack.pop()
	                if p == -1:
	                    if len(path) > len(longest):
	                        longest = list(path)
	                    path.pop()
	                    continue
	                path.append(p)
	                new = set(e[p]) - set(path)
	                stack += [-1] + list(new)
	
	            return longest
	        longest = longPath(u)
	        v = longest[-1]
	        longest = longPath(v)
	        m = len(longest)
	        if m % 2 == 1:
	            ans = [longest[m/2]]
	        else:
	            ans = [longest[m/2], longest[m/2 - 1]]
	        return ans
	
---

	class Solution(object):
	    def findMinHeightTrees(self, n, edges):
	        """
	        :type n: int
	        :type edges: List[List[int]]
	        :rtype: List[int]
	        """
	        if not edges: return [0]
	        from collections import defaultdict
	        e = defaultdict(set)
	        for v,w in edges:
	            e[v].add(w)
	            e[w].add(v)
	        leaves = set([v for v in e if len(e[v]) == 1])
	        while n > 2:
	            n -= len(leaves)
	            new = set([])
	            for v in leaves:
	                for w in e[v]:
	                    e[w].remove(v)
	                    if len(e[w]) == 1:
	                        new.add(w)
	            leaves = new
	
	        return list(leaves)     

		