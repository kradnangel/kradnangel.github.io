---
layout: post
title: LeetCode_001_Two Sum
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2

###Solution
First, we use the target to minus every element in the *nums* to get a new list. If there are two numbers that are added up to target, they must be in both lists. Thereform, we get the intersection of two lists(convert them to set firstly) as the solution list.

There are three cases:

1. only one number: there must be two same numbers that are added up to target.
2. two numbers: just find the index of these two numbers.
3. three nummbers: there must be one numbers which equals to half of the target. And because there is only one solution for the target. So, this number must be only one in the list instead of two. In which case, this number is not part of solution. So, we need to remove it from the solution list.

Last, just return the indexes in order.



###Code
	class Solution:
        # @param {integer[]} nums
        # @param {integer} target
        # @return {integer[]}
        def twoSum(self, nums, target):
            minus = []
            for x in nums:
            	minus.append(target - x)

            setn = set(nums)
            setm = set(minus)
            inter = setn & setm
            listi = list(inter)
            if len(listi) == 3:
            	for x in listi:
            		if x+x == target:
            			rem = x
            			break
            	listi.remove(rem)
            index1 = nums.index(listi[0]) + 1
            if len(listi) == 2:
            	index2 = nums.index(listi[1]) + 1
            else:
            	nums.remove(listi[0])
            	index2 = nums.index(listi[0]) + 1 + 1

            if index2 < index1:
            	return index2, index1
            else:
            	return index1, index2