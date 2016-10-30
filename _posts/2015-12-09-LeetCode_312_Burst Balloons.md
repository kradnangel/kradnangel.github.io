---
layout: post
title: LeetCode_312_Burst Balloons
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
### [Question](https://leetcode.com/problems/burst-balloons/)

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

    
### Solution

DP.

a[i][j] means the maximum value of bursting all balloons in [i,j].

	a[i][j] = max(a[i][j], a[i][k] + nums[i] * nums[k] * nums[j] + a[k][j])


i is the left boundary

j is the right boundary

k is the midpoint which balloon is bursted at last.

### Code

code: {% gist f1bd27ed6bda63a27b739f9415fbdd70 %}