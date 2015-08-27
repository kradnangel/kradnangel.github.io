---
layout: post
title: LeetCode_033_Search in Rotated Sorted Array
categories: [LeetCode]
tags: [LeetCode, python, sort]
fullview: true
---
###Question
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

###Solution
The key method is dichotomy.

The array is in ascending order, but it is also rotated.

So, when we divide this array in two arrays, there must be a array which is in ascending order. 

Thereform, there are several cases:

1. target == mid
	return the index of mid
2. target <  mid
	1. [left : mid] is in ascending order(nums[left] <= nums[mid]) and 	target > left
	The target is in [left : mid]
	2. [left : mid] is in ascending order(nums[left] <= nums[mid]) and 	target < left
	The target is in [mid : right]
	3. [right : mid] is in ascending order(nums[left] > nums[mid])
	The target is in [left : mid]

3. target >  mid
	It is similar as "target < mid". It also has 3 cases.


###Code
	class Solution(object):
        def search(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            left = 0
            right = len(nums) - 1
            ans = -1

            while left <= right:    
                mid = (left + right) / 2
                if target == nums[mid]:
                    ans = mid
                    break
                elif target < nums[mid]:
                    if (target < nums[left]) and (nums[left] <= nums[mid]):
                        left = mid + 1
                    else:
                        right = mid - 1
                elif target > nums[mid]:
                    if (target > nums[right]) and (nums[mid] <= nums[right]):
                        right = mid - 1
                    else:
                        left = mid + 1

            return ans