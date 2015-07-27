---
layout: post
title: LeetCode_067_Add Binary
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given two binary strings, return their sum (also a binary string).

For example,

a = "11"

b = "1"

Return "100".

###Solution
First, because the lengths of two string are different. We need to add some '0' to the head of the shorter string.

Second, from the tail of the two string, we try to add them together and use 'carry' to hold the carry bit.

At last, we need to check the carry bit is 1 or 0. If it's 1, we need to add one more '1' to the head of answer string.


###Code
	class Solution:
        # @param {string} a
        # @param {string} b
        # @return {string}
        def addBinary(self, a, b):
            la = len(a)
            lb = len(b)
            if la > lb:
                b = '0' * (la - lb) + b
            else:
                a = '0' * (lb - la) + a

            lmax = max(la, lb)
            lans = 0
            carry = 0
            ans = ""
            while lans < lmax:
                carry = int(a[lmax - lans - 1]) + int(b[lmax - lans - 1]) + carry
                #print a[lmax - lans - 1], (b[lmax - lans - 1])
                ans = str(carry % 2) + ans
                carry = carry / 2
                lans += 1
                
                
            if carry > 0:
                ans = '1' + ans

            return ans