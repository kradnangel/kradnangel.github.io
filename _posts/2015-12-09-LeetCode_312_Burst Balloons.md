---
layout: post
title: LeetCode_312_Burst Balloons
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###[Question](https://leetcode.com/problems/burst-balloons/)
Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

Note: 

(1) You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.
(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

Example:

Given [3, 1, 5, 8]

Return 167

    nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
    coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167

    
###Solution
DP.

a[i][j] means the maximum value of bursting all balloons in range(i+1,j+1). Not include the boundary.

	a[i][j] = max(a[i][j], a[i][k] + nums[i] * nums[k] * nums[j] + a[k][j])

m is the range

i is the left boundary

j = i + m -1 is the right boundary

k is the midpoint which balloon is bursted at last.

###Code
	class Solution(object):
        def maxCoins(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            nums.append(1)
            nums.insert(0,1)
            n = len(nums)
            r = xrange(n)
            a = [[0 for k in r] for j in r]
            for i in r:
                a[i][i] = nums[i]

            for m in xrange(3,n+1):
                for i in xrange(n-m+1):
                    j = i + m - 1
                    for k in xrange(i+1,j):
                        a[i][j] = max(a[i][j], a[i][k] + nums[i]*nums[k]*nums[j] + a[k][j])

            return a[0][n-1]