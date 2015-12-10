---
layout: post
title: LeetCode_310_Minimum Height Trees
categories: [LeetCode]
tags: [LeetCode, python, stack]
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

###Solution
Simplest idea is to try to set every node as the root and then check the height. But, not surprisingly, time limit exceeded.

The second idea is finding the longest path in this undirected graph and find the midpoint of this path. So, the answer should include one or two nodes. 

This method is ok. It cost 1013ms to finish all cases. But, it is not fast enough. 

The third idea is deleting leaves over and over again. When only one or two nodes are remained, stop and output.


###Code
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