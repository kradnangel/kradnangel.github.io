---
layout: post
title: LeetCode_090_Subsets II
categories: [LeetCode]
tags: [LeetCode, python, set]
fullview: true
---
###Question
Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note:

Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,
If nums = [1,2,2], a solution is:

	[
	  [2],
	  [1],
	  [1,2,2],
	  [2,2],
	  [1,2],
	  []
	]
	
###Solution
Based on the program of "Subsets", just delete the duplicate subsets.


###Code
	class Solution(object):
        def subsetsWithDup(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            nums.sort()
            l = len(nums)
            ans = []
            ans.append([])

            for i in range(1,l):	# length = 1,2,3 ... l-1
            	a = [h for h in range(i)]	# [0, 1, 2 ... i - 1]
            	j = i - 1	# point to the tail
            	while j >= 0:
            		b = [nums[h] for h in a]
            		# The new part
            		if b not in ans:
            			ans.append(b)
            		# ------------
            		while (j >= 0) and (a[j]+1 > l - i + j):
            			j -= 1
            		if j < 0: break
            		else: 
            			a[j] += 1
            			for h in range(j+1, i):
            				a[h] = a[h-1] + 1
            			j = i - 1    			

            ans.append(nums)
            return ans