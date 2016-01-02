---
layout: post
title: LeetCode_210_Course Schedule II
categories: [LeetCode]
tags: [LeetCode, python, graph, Topological sorting]
fullview: true
---
###[Question](https://leetcode.com/problems/course-schedule-ii/)
There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:

	2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]
	
	4, [[1,0],[2,0],[3,1],[3,2]]
There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].

Note:

The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

### Solution
The same idea with [Course Schedule](http://qianrenzhou.me/leetcode/2016/01/01/LeetCode_207_Course%20Schedule.html). Use directed graph to represent the relasionship among courses and use topological sorting to generate one valid order. 
           
### Code
	from collections import defaultdict
    class Solution(object):
        def findOrder(self, numCourses, prerequisites):
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
            for s,f in cs:
                d[f].append(s)
                ind[s] = ind.get(s,0) + 1
                connectedNodes.add(f)
                connectedNodes.add(s)
            zero, ans = [],list(set(range(0,n)) - connectedNodes)
            m = len(connectedNodes)
            for v in connectedNodes:
                if not ind.get(v):
                    zero.append(v)
            while zero:
                u = zero.pop()
                ans.append(u)
                m -= 1
                for v in d[u]:
                    ind[v] -= 1
                    if ind[v] == 0:
                        zero.append(v)
            return ans if m == 0 else []