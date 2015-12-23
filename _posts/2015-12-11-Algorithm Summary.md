---
layout: post
title: Algorithm Summary
categories: [Algorithm]
tags: [Algorithm]
fullview: true
---

## Dynamic Programming

### Precondition
The question should satisfy following three principles:

1. Superior sub-structure property: The best strategy of original question could also be used in sub-questions to get best answer.

2. [Unfollow-up effect](http://baike.baidu.com/view/2862466.htm): When a question is divided into several decision phases, the former decision phases won't affect the posterior decision phases, except by state transition equation.

3. Superposition of sub-questions


### Classification

#### 2D direct model

##### Model
Given two strings/lists.
 
a[i][j] means the result of combining s1[:i-1] and s2[:j-1].

a[n][m] is the final answer for original question.

##### Complexity
O(n^2)

##### Algorithm Framework

	#initialization
	n, m = len(s1), len(s2)
	a = [[0/False for col in xrange(n)] for row in xrange(m)]
	'Calculate a[0][0] and so on'
	for i in xrange(1, n):
		for j in xrange(1, m):
			a[i][j] = ... #State transition equation
	return a[n][m]
	
##### Examples
[Interleaving String](http://qianrenzhou.me/leetcode/2015/09/08/LeetCode_097_Interleaving%20String.html)

[Regular Expression Matching](http://qianrenzhou.me/leetcode/2015/12/13/LeetCode_010_Regular%20Expression%20Matching.html)



#### 2D sectional model / insertion model

##### Model
Given one string / list.

a[i][j] means the best result of s[i:j]

a[0][n-1] is the best answer of original question.

Generally, enumerate the range, the left point and the midpoint. 

##### Complexity
O(n^3)

##### Algorithm Framework

	#initialization
	n = len(s)
	a = [[0 for col in xrange(n)] for row in xrange(n)]

	for i in xrange(n):
		'initial a[i][i]' #e.g. a[i][i] = s[i]	
		
	for 'range m' in xrange(n):
		for 'left point i' in xrange(n-m+1):
			j = i + m - 1
				for 'midpoint k' in xrange(i+1,j):
				# When enumerate the k, pay attention to the boundary conditions
				a[i][j] = ... #e.g. max(a[i][k], a[k][j])
				
	return a[0][n-1]
				

###Searching

####Depth First Search

#####Algorithm Framework

	def dfs(x):
		if 'reach the target':
			save answer
			return
		elif 'could be pruned':
			return
		for i in xrange('width of searching'):
			'backup'
			dfs('new x')
			'recover'
		
#####Pruning optimization 

1. Optimization pruning: Current searing result couldn't be better than current best answer.

2. Memorizing pruning: Return corresponding answer stored/Exit when current state has been searched before. 

3. Repeatability pruning: Narrow the width of searching by checking that following searching would be the same as other searching or not. (9-4-1 vs. 4-9-1)

4. Feasibility pruning: If current state couldn't lead to a solution, exit.

5. Changing Searching order: Search the space which have more possibility to get the best answer first. 
	1. [Lowest-Cost-First Search](http://www.cs.ubc.ca/~mack/CS322/lectures/2-Search6.pdf) (LCFS) (g(n))
	2. [Best-First Search](https://en.wikipedia.org/wiki/Best-first_search)				(h(n))

6. preprocessing: preprocess to get a initial solution first. It could be used as the threshold of optimization pruning. The common method to get a initial solution is greedy algorithm.






