---
layout: post
title: LeetCode_055_Jump Game
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:

A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

###Solution
The first idea is using a list to show every position is reachable or not. Then scan the list from the beginning. 

However, this method is too time consuming.

Because, if k is reachable, k-1 must be reachable. So, we can just use a variable to show that behind this position, all the positions are unreachable.

Then scan the list and judge the current position could reach the next unreachable position or not. Then update the next unreachable position.

At last, after scanning the whole list, judge that whether the next unreachable position is bigger than the length of list or not. If yes, it means the last position is reachable. Then return True. Otherwise, return False.

###Code
	class Solution:
		# @param {integer[]} nums
		# @return {boolean}
		def canJump(self, nums):
			n = len(nums)
			if n == 1:
				return True
			noreach = 1 #the index which is no reach
			now = 0		#the current index
			for x in nums:	#the jumps
				if (now < noreach) & (x > 0):
					if (now + x >= noreach):
	   					noreach = now + x + 1
	   				
	   			now += 1

			return (noreach >= n)