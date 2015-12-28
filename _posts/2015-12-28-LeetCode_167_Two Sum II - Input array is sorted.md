---
layout: post
title: LeetCode_167_Two Sum II - Input array is sorted
categories: [LeetCode]
tags: [LeetCode, python, Dichotomy]
fullview: true
---
###[Question](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2

### Solution
The array is sorted. So, we can use two pointers to point the two numbers separately. The first pointer start at position 0 and move toward right. The second pointer start at position n-1 and move toward left. 

Basic idea is move one pointer one step every time. If the sum of two numbers pointed by pointers is larger than target, move the second pointer one step left. If the sum is smaller than the target, move the first pointer one step right. 

It works and the time complexity is O(n) on the worst case.

One improvement is that we can try to move the pointer to the midpoint of the two pointers every time. But, we need to check the sum after moving. We should make sure that after moving, the sum is still larger/smaller than the target. The orignal sum is larger, then after moving the sum should also be larger. This could make sure that we won't miss the right numbers.

The average time complexity is O((log n)^2)
           
### Code
	class Solution(object):
        def twoSum(self, numbers, target):
            """
            :type numbers: List[int]
            :type target: int
            :rtype: List[int]
            """
            x, y = 0, len(numbers) - 1
            while x < y:
                m = (x+y)/2
                sums = numbers[x] + numbers[y] 
                if sums == target:
                    return [x+1,y+1]
                elif sums > target:
                    while (m < y - 1) and (numbers[x] + numbers[m] < target):
                        m = (m + y) / 2
                    y = m
                elif sums < target:
                    while (m > x + 1) and (numbers[m] + numbers[y] > target):
                        m = (x + m) / 2
                    x = m
                    