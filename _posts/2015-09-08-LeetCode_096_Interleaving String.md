---
layout: post
title: LeetCode_096_Interleaving String
categories: [LeetCode]
tags: [LeetCode, python, string, DP]
fullview: true
---
###Question
Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

For example,

Given:

s1 = "aabcc",

s2 = "dbbca",

When s3 = "aadbbcbcac", return true.

When s3 = "aadbbbaccc", return false.


###Solution
DP.

Because we need to find whether s3 is formed by the interleaving of s1 and s2, we can design a state transition equation.

a[i][j] means whether s3[0:i+j] is formed by the interleaving of s1[0:i] and s2[0:j].

Therefore, we design the state transition equation:

	a[i][j] = (a[i-1][j] & (s1[i-1] == s3[i-1+j])) or (a[i][j-1] & (s2[j-1] == s3[j-1+i]))

means that we have two cases. s3[0:i+j] can be formed by s1[0:i-1] + s[i] and s2[0:j] or s1[0:i] and s2[0:j-1] + s2[j].

So, a[len(s1)][len(s2)] will be the right answer.

###Code
	class Solution(object):
	    def isInterleave(self, s1, s2, s3):
	        """
	        :type s1: str
	        :type s2: str
	        :type s3: str
	        :rtype: bool
	        """
	        
	        n = len(s1)
	        m = len(s2)
	        if m+n != len(s3): return False
	        if n == 0: return (cmp(s2,s3) == 0)
	        if m == 0: return (cmp(s1,s3) == 0)
	        a = [[False for j in range(m+1)] for i in range(n+1)]
	        a[0][0] = True
	        for i in range(1, n+1):
	            a[i][0] = a[i-1][0] & (s1[i-1] == s3[i-1])
	            print a[i][0]
	        for j in range(1, m+1):
	            a[0][j] = a[0][j-1] & (s2[j-1] == s3[j-1])
	            print a[0][j]

	        for i in range(1, n+1):
	            for j in range(1, m+1):
	                a[i][j] = (a[i-1][j] & (s1[i-1] == s3[i-1+j])) or (a[i][j-1] & (s2[j-1] == s3[j-1+i]))
	        

	        return a[n][m]