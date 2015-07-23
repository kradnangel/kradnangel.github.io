---
layout: post
title: LeetCode_064_Minimum Path Sum
categories: [LeetCode]
tags: [LeetCode, python, grid]
fullview: true
---
###Question
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

###Solution
There are two ways to get to a point, from above or from left. So, the minimum path to current point is current number add the smaller one of the path to above and the path to the left.

###Code
	class Solution:
		# @param {integer[][]} grid
		# @return {integer}
		def minPathSum(self, grid):
			m = len(grid)
			n = len(grid[0])
			for i in range(1, m):
				grid[i][0] += grid[i-1][0]
			for j in range(1, n):
				grid[0][j] += grid[0][j-1]
			for i in range(1,m):
				for j in range(1,n):
					grid[i][j] += min(grid[i-1][j], grid[i][j-1])
			return grid[m-1][n-1]