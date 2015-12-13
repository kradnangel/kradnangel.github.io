---
layout: post
title: LeetCode_240_Search a 2D Matrix II
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###[Question](https://leetcode.com/problems/search-a-2d-matrix-ii/)
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.
For example,

Consider the following matrix:

	[
	  [1,   4,  7, 11, 15],
	  [2,   5,  8, 12, 19],
	  [3,   6,  9, 16, 22],
	  [10, 13, 14, 17, 24],
	  [18, 21, 23, 26, 30]
	]

Given target = 5, return true.

Given target = 20, return false.

    
###Solution
The idea is that binary search the elements of main diagonal to find one elements is larger a bit or equal to target. Let's say larger. So, the matrix could be divided into four part. The elements in top left part are all samller than target, while the elements in bottom right part are all larger than target. The target may locate in the top right part and bottom left part. So, we just repeat the binary searching in the main diagonal in the two remaining parts.


###Code
	class Solution(object):
        def searchMatrix(self, matrix, target):
            """
            :type matrix: List[List[int]]
            :type target: int
            :rtype: bool
            """
            def check(t,b,l,r):    
                n,m = b-t+1, r-l+1
                ans = False
                if n == 1:          
                    x,y = 0,m-1
                    while y>x:
                        i = (y+x)/2            
                        if matrix[t][l+i] < target:
                            x = i+1
                        elif matrix[t][l+i] > target:
                            y = i
                        else:
                            ans = True
                            break                
                    ans = ans or (matrix[t][l+x] == target)
                elif m == 1:  
                    x,y = 0,n-1
                    while y>x:
                        i = (y+x)/2            
                        if matrix[t+i][l] < target:
                            x = i+1
                        elif matrix[t+i][l] > target:
                            y = i
                        else:
                            ans = True
                            break                
                    ans = ans or (matrix[t+x][l] == target)
                else:
                    nm = min(n,m)
                    x,y = 0,nm-1
                    while y>x:
                        i = (y+x)/2            
                        if matrix[t+i][l+i] < target:
                            x = i+1
                        elif matrix[t+i][l+i] > target:
                            y = i
                        else:
                            ans = True
                            break
                    i = x        
                    ti,li = t+i,l+i
                    if not ans:
                        if (i == 0) and (matrix[ti][li] != target):
                            ans = False
                        elif (i == nm) or ((i<nm) and (matrix[ti][li] < target)):
                            if n < m:
                                ans = check(t,b,li+1,r)
                            elif n > m:
                                ans = check(ti+1,b,l,r)
                            else:
                                ans = False                
                        elif matrix[ti][li] == target:
                            ans = True
                        elif matrix[ti][li] > target:
                            ans = check(t,ti-1,li,r) or check(ti,b, l,li-1)

                return ans    

            n = len(matrix)
            if n == 0: return False
            m = len(matrix[0]) 
            return check(0,n-1,0,m-1)   