---
layout: post
title: LeetCode_053_Maximum Subarray
categories: [LeetCode]
tags: [LeetCode, python, DP]
fullview: true
---
###[Question](https://leetcode.com/problems/maximum-subarray/)
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [−2,1,−3,4,−1,2,1,−5,4],

the contiguous subarray [4,−1,2,1] has the largest sum = 6.

### Solution
DP.

Maximum in range [0, i] is the max of (current value or maximum in range [0, i-1] plus current value).


### Code
{% gist c9e9b0b42d48fa70e07f %}          