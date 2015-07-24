---
layout: post
title: LeetCode_066_Plus One
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

###Solution
High precision addition.


###Code
	class Solution:
	    # @param {integer[]} digits
	    # @return {integer[]}
	    def plusOne(self, digits):
	    	carry = 0
	    	l = len(digits)
	    	carry = (digits[l-1] + 1) / 10
	    	digits[l-1] = (digits[l-1] + 1) % 10
	        for i in range(l-2,-1,-1):
	        	digits[i] += carry
	        	carry = digits[i] / 10
	        	digits[i] %= 10
	        if carry > 0:
	        	digits = [carry] + digits

	        return digits