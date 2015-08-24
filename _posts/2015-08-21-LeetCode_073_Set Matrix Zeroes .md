---
layout: post
title: LeetCode_073_Set Matrix Zeroes 
categories: [LeetCode]
tags: [LeetCode, python, matrix]
fullview: true
---
###Question
Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

Follow up:

Did you use extra space?
A straight forward solution using O(mn) space is probably a bad idea.

A simple improvement uses O(m + n) space, but still not the best solution.

Could you devise a constant space solution?

###Solution
The key question is how to save space.
A easy way to solve problem is using a list to mark which row should be set as 0 and another one to mark which column should be set as 0.

The improved method is using the first row and first column to mark and just using two more space to mark the first row and first column should be set as 0 or not.


###Code
	class Solution(object):
	    def setZeroes(self, matrix):
	        """
	        :type matrix: List[List[int]]
	        :rtype: void Do not return anything, modify matrix in-place instead.
	        """
	        row = len(matrix)
	        col = len(matrix[0])

	        fstrow = 0 in matrix[0]
	        fstcol = False
	        for i in range(row):
	        	if matrix[i][0] == 0:
	        		fstcol = True
	        		break

	        for i in range(1, row):
	        	for j in range(1, col):
	        		if matrix[i][j] == 0:
	        			matrix[0][j] = 0
	        			matrix[i][0] = 0

	        for j in range(1, col):
	        	if matrix[0][j] == 0:
	        		for i in range(1, row):
	        			matrix[i][j] = 0

	        for i in range(1, row):
	        	if matrix[i][0] == 0:
	        		for j in range(1, col):
	        			matrix[i][j] = 0

	        if fstrow:
	        	for j in range(col):
	        		matrix[0][j] = 0

	        if fstcol:
	        	for i in range(row):
	        		matrix[i][0] = 0