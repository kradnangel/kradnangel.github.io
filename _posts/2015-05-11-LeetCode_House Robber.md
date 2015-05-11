---
layout: post
title: LeetCode_House Robber
categories: [LeetCode]
tags: [LeetCode, python, DP]
fullview: true
---
###Question
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

###Solution
There are only two choices for every house -- rob or not rob. So, we can define 'rob0' as do not rob current house and define 'rob1' as rob current house. And we begin at the first house and end at the last house.

So, if rob the current house, we can't rob the prior one. So, the current maximum is the sum of 'rob0' and the amount of money of current house.

If do not rob the current house, the current maximum is 'do not rob the prior one' or 'rob the prior one'.


###Code
	class Solution:
	    # @param {integer[]} nums
	    # @return {integer}
	    def rob(self, nums):
	    	n = len(nums)
	    	rob0 = 0
	    	rob1 = 0
	    	for i in range(0,n):
	    		t = rob0
	    		rob0 = max(rob0, rob1)
	    		rob1 = t + nums[i]
	    	return max(rob0, rob1)