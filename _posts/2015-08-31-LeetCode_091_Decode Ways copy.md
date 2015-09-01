---
layout: post
title: LeetCode_091_Decode Ways
categories: [LeetCode]
tags: [LeetCode, python, code]
fullview: true
---
###Question
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.
	
###Solution
The first idea is that we can solve it like what we do in question "Subsets". We can enumerate every case and count. However, it will be too slow to pass the test.

A better idea is that, we can find that if we know the number of ways decoding a string and add a number before this string, the number of ways decoding the new string can be confirmed. 

If the number added before the old string cannot combine with the first number of the old string to make a new char, the number of ways decoding the new string euqals the number of ways decoding the old string. 

If the two numbers can make a new char, then the numbers of ways decoding euqals the numbers of ways decoding the old string (means we take the number added as a single number which represent a char) plus the numbers of ways decoding the old string without the first number (means we take the number added and the first number of the old string as a entirety to represent a char). 

Be careful with dealing with the number "0". When the numbers added is "0", the number of ways decoding new string is 0.

Some special cases:

""

"0"

"01"

"101"

"230"



###Code
	class Solution(object):
	    def numDecodings(self, s):
	        """
	        :type s: str
	        :rtype: int
	        """
	        if (s == "") or (s[0] == "0"):
	        	return 0
	        n = len(s)
	        a = [1]
	        if s[-1] == "0":
	        	a.append(0)
	        else:
	        	a.append(1)
	        second = ["0","1","2","3","4","5","6"]
	        for k in range(n-2, -1, -1):
	            if (s[k] == "1") or ((s[k] == "2") and (s[k+1] in second)):
	                a.append(a[-1]+a[-2])
	            elif s[k] == "0":
	                a.append(0)
	            else:
	            	a.append(a[-1])
	            print k,s[k],s[k+1]
	        
	        return a[-1]