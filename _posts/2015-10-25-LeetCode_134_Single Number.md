---
layout: post
title: LeetCode_134_Single Number
categories: [LeetCode]
tags: [LeetCode, python, Numerical, Bit Manipulation]
fullview: true
---
###Question
Given an array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

###Solution
Just xor all numbers together and return it. 
Because the result of xor of two same numbers is 0.

###Code
	class Solution(object):
        def singleNumber(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            for x in nums[1:]:
                nums[0] = nums[0] ^ x
            return nums[0]