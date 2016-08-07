---
layout: post
title: LeetCode_371_Sum of Two Integers
categories: [LeetCode]
tags: [LeetCode, python, Bit Manipulation]
fullview: true
---
### [Question](https://leetcode.com/problems/sum-of-two-integers/)
Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:
Given a = 1 and b = 2, return 3.

### Solution
Bit Manipulation.

a xor b, get plus without carry.

(a and b) << 1, get carry.

For python, 'Thus the number -5 is treated by bitwise operators as if it were written "...1111111111111111111011".' So, we need to use mask = 0xffffffff to make numbers within int range. If the result is negetive, we need to trun it over twice to convert it to python complement negative.


### Code
{% gist 7e26053f5bba329614713d185b390f1b %}          