---
layout: post
title: LeetCode_054_Spiral Matrix
categories: [LeetCode]
tags: [LeetCode, python, matrix]
fullview: true
---
###Question
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:
	
	[
	 [ 1, 2, 3 ],
	 [ 4, 5, 6 ],
	 [ 7, 8, 9 ]
	]

You should return [1,2,3,6,9,8,7,4,5].

###Solution
The key point is using a symbol as this position has been visited.

Here, we can use a point (i,j) to scan the whole matrix in a special order.

This the scanning, use a 2D-list to set the direction of the move of the point. First, go right[0,1]. Second, go down[1,0]. Third, go left[0,-1]. Last, go up[-1,0].

Scan the whole matrix till all numbers have been visited.

###Code
	class Solution:
	    # @param {integer[][]} matrix
	    # @return {integer[]}
	    def spiralOrder(self, matrix):
	    	if matrix == []:
	    		return []
	        m = len(matrix)
	        n = len(matrix[0])
	        i = 0
	        j = 0
	        direct = [[0,1],[1,0],[0,-1],[-1,0]]
	        now = 0
	        count = 0
	        ans = []
	        while count < m*n:
	        	while (0 <= i < m) & (0 <= j < n):
	        		if matrix[i][j] == 'm':
	        			break
	        		ans.append(matrix[i][j])
	        		
	        		matrix[i][j] = 'm'
	        		i += direct[now][0]
	        		j += direct[now][1]
	        		count += 1
	        	i -= direct[now][0]
	        	j -= direct[now][1]
	        	now = (now + 1) % 4
	          	i += direct[now][0]
	        	j += direct[now][1]      	

	        return ans