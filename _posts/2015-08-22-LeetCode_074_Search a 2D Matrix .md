---
layout: post
title: LeetCode_074_Search a 2D Matrix
categories: [LeetCode]
tags: [LeetCode, python, matrix]
fullview: true
---
###Question
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
For example,

Consider the following matrix:

	[
		[1,   3,  5,  7],
		[10, 11, 16, 20],
		[23, 30, 34, 50]
	]

Given target = 3, return true.


###Solution
Compare the number with the elements in the matrix from top to bottom and from left to right.

###Code
	class Solution(object):
	    def searchMatrix(self, matrix, target):
	        """
	        :type matrix: List[List[int]]
	        :type target: int
	        :rtype: bool
	        """
	        
	        i = 0
	        j = 0
	        n = len(matrix)
	        m = len(matrix[0])

	        while target > matrix[i][j]:
	        	i += 1
	        	if i == n:
	        		i -= 1
	        		break

	        if target == matrix[i][j]:
	        	return True	
	        elif target < matrix[i][j]:
	        	i -= 1

	        while target > matrix[i][j]:
	        	j += 1
	        	if j == m:
	        		j -= 1
	        		break

	        if target == matrix[i][j]:
	        	return True
	        else: return False