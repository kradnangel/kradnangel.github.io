---
layout: post
title: LeetCode_058_Length of Last Word
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 

Given s = "Hello World",

return 5.

###Solution
First, reverse the string.

Second, delete the blanks which is in the beginning.

Third, find the location of first blank in the remaining string.

At last, if there is no blank, return the length of remaining string. Otherwise, return k which means the length of the last word.

###Code
	class Solution:
        # @param {string} s
        # @return {integer}
        def lengthOfLastWord(self, s):
        	a = s[::-1]
            while len(a) > 0:
                if a[0] == ' ':
                    a = a[1:]
                else:
                    break
            k = a.find(' ')
            if k == -1:
                return len(a)
            else:
                return k