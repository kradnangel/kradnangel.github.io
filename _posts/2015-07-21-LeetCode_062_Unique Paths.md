---
layout: post
title: LeetCode_062_Unique Paths
categories: [LeetCode]
tags: [LeetCode, python, grid]
fullview: true
---
###Question
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

Note: m and n will be at most 100.

###Solution
The paths to current position are the sum of the paths to the above of current position and the paths to the left of current position.


###Code
	class Solution:
	    # @param {integer} m
	    # @param {integer} n
	    # @return {integer}
	    def uniquePaths(self, m, n):
	        a = [[0 for col in range(n)] for row in range(m)]
	        for i in range(m):
	        	a[i][0] = 1
	        for j in range(n):
	        	a[0][j] = 1
	        for i in range(1,m):
	        	for j in range(1,n):
	        		a[i][j] = a[i-1][j] + a[i][j-1]
	        return a[m-1][n-1]