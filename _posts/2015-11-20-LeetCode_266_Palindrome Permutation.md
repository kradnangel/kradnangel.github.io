---
layout: post
title: LeetCode_266_Palindrome Permutation
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a string, determine if a permutation of the string could form a palindrome.

For example,

"code" -> False, "aab" -> True, "carerac" -> True.
    
###Solution
Two cases of palindrome:
1. 12321
2. 1221

Use hashmap (dictionary in python) to count each char.
If the number of odd frequency numbers is less than 2, return Ture.


###Code
	class Solution(object):
        def canPermutePalindrome(self, s):
            """
            :type s: str
            :rtype: bool
            """
            d = {}
            for c in s: 
                d[c] = d.get(c,0) + 1
            sum = 0
            for c in d: 
                if d[c] % 2 != 0: sum += 1
            return sum < 2