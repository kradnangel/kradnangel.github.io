---
layout: post
title: LeetCode_059_Spiral Matrix II
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given an integer n, generate a square matrix filled with elements from 1 to n<sup>2</sup> in spiral order.

For example,

Given n = 3,

You should return the following matrix:

	[
		[ 1, 2, 3 ],
		[ 8, 9, 4 ],
		[ 7, 6, 5 ]
	]

###Solution
The method is the same as that used in question "Spiral Matrix". Use a list to save the four direction and use a point to follow the sprial order. 

Key point: The initialization of 2D list.

2DList = [[0 for col in range(m)] for row in range(n)]

###Code
	class Solution:
	    # @param {integer} n
	    # @return {integer[][]}
	    def generateMatrix(self, n):
	        ans = [[0 for col in range(n)] for row in range(n)]
	        i = 0
	        j = 0
	        direct = [[0,1],[1,0],[0,-1],[-1,0]]
	        now = 0
	        count = 0
	        while count < n*n:
	        	while (0 <= i < n) & (0 <= j < n):
	        		if ans[i][j] != 0:
	        			break
	        		count += 1
	        		ans[i][j] = count
	        		i += direct[now][0]
	        		j += direct[now][1]
	        		
	        	i -= direct[now][0]
	        	j -= direct[now][1]
	        	now = (now + 1) % 4
	          	i += direct[now][0]
	        	j += direct[now][1]  
	        		

	        return ans