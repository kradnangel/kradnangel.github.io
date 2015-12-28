---
layout: post
title: LeetCode_001_Two Sum
categories: [LeetCode]
tags: [LeetCode, python, hash]
fullview: true
---
###[Question](https://leetcode.com/problems/two-sum/)
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2

### Solution
We should notice some special cases first.

1. Numbers can be duplicate.
2. Numbers are not sorted at first

Then, the idea is that scan the list from the beginning. Then save the value 'x' in a hash table (key = 'x', value = index) one by one. So, all the numbers appeared in hash table are visited. When scanning, check whether the 'target - x' is in the hash table or not. If yes, return the indexs. In this case, it could deal with the case like"[1,2,3],6".
 
The worst-case time-complexity of this algorithm is of O(n). But, generally, the time spent is less than O(n).
           
### Code
	class Solution(object):
        def twoSum(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: List[int]
            """
            d = {}
            for i,x in enumerate(nums):
                if target-x in d:
                    return [d[target-x], i+1]
                d[x] = i+1
