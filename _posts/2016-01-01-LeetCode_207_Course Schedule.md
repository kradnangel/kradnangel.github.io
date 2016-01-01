---
layout: post
title: LeetCode_207_Course Schedule
categories: [LeetCode]
tags: [LeetCode, python, graph, Topological sorting]
fullview: true
---
###[Question](https://leetcode.com/problems/course-schedule/)
There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:

	2, [[1,0]]

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

	2, [[1,0],[0,1]]

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

Note:

The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

### Solution
A basic question about using Topological sorting to solve a graph problem.

prerequisites are edges. Based on these, construct a directed graph by using adjacency list. What's more, using a hash table to record the indegree of every nodes. 

After constructing the graph, try to find the Topological sorting of this graph. If Topological sorting of this graph exists, return yes. Otherwise, return false.          
           
### Code
	from collections import defaultdict
    class Solution(object):
        def canFinish(self, numCourses, prerequisites):
            """
            :type numCourses: int
            :type prerequisites: List[List[int]]
            :rtype: bool
            """
            n = numCourses
            cs = prerequisites
            d = defaultdict(list)
            ind = {}
            connectedNodes = set([])
            for f,s in cs:
                d[f].append(s)
                ind[s] = ind.get(s,0) + 1
                connectedNodes.add(f)
                connectedNodes.add(s)
            zero = []
            m = len(connectedNodes)
            for v in connectedNodes:
                if not ind.get(v):
                    zero.append(v)
            while zero:
                u = zero.pop()
                m -= 1
                for v in d[u]:
                    ind[v] -= 1
                    if ind[v] == 0:
                        zero.append(v)
            return m == 0     
 