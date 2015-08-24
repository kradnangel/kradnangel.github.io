---
layout: post
title: LeetCode_078_Subsets
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a set of distinct integers, nums, return all possible subsets.

Note:

Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,

If nums = [1,2,3], a solution is:

	[
	  [3],
	  [1],
	  [2],
	  [1,2,3],
	  [1,3],
	  [2,3],
	  [1,2],
	  []
	]

###Solution
At first, sort the list. 

Add the first subset, empty set.

Then, start to enumerate subsets of every length.

In every length i, we enumerate positions instead of specific elements. That is:

	nums:		[3,5,6,8,9]
	position:	[0,1,2,3,4]

Besides, in every length i, we start at [0,1,2 .. i-1]. That is:

	i = 3
	a = [0,1,2]

Then we add 1 to the tail till the tail reaches the bound.

	[0,1,3]
	[0,1,4]

Then we add 1 to the position before the tail and reset the value of every position after the current position. Set the value one more than the value of the position before this position.

	[0,2,3]
	
Then repeat. Add 1 to the tail till the tail reaches the bound.

	[0,2,4]
	
Finally, we can find all all possibilities.



###Code
	class Solution(object):
	    def subsets(self, nums):
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
	        		ans.append(b)
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