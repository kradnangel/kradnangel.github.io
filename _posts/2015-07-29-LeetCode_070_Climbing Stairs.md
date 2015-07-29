---
layout: post
title: LeetCode_070_Climbing Stairs
categories: [LeetCode]
tags: [LeetCode, python, numbers]
fullview: true
---
###Question
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

###Solution
Fibonacci Sequence

[1] = 1

[2] = 2

[3] = [1] + [2]

...

[k] = [k-1] + [k-2]

###Code
	class Solution:
	    # @param {integer} n
	    # @return {integer}
	    def climbStairs(self, n):
	        if n == 1:
	        	return 1
	        elif n == 2:
	        	return 2
	        else:
	        	i = 1
	        	j = 2
	        	count = 2
	        	while count < n:
	        		count += 1
	        		t = j
	        		j = i + j
	        		i = t
	        	return j