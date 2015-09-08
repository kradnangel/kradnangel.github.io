---
layout: post
title: LeetCode_087_Scramble String
categories: [LeetCode]
tags: [LeetCode, python, DP]
fullview: true
---
###Question
Given a string s1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

Below is one possible representation of s1 = "great":

	    great
	   /    \
	  gr    eat
	 / \    /  \
	g   r  e   at
	           / \
	          a   t
	          
To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node "gr" and swap its two children, it produces a scrambled string "rgeat".

	    rgeat
	   /    \
	  rg    eat
	 / \    /  \
	r   g  e   at
	           / \
	          a   t	          
	          
We say that "rgeat" is a scrambled string of "great".

Similarly, if we continue to swap the children of nodes "eat" and "at", it produces a scrambled string "rgtae".

	    rgtae
	   /    \
	  rg    tae
	 / \    /  \
	r   g  ta  e
    	   / \
		  t   a	          
	          
We say that "rgtae" is a scrambled string of "great".

Given two strings s1 and s2 of the same length, determine if s2 is a scrambled string of s1.


###Solution
3D DP + pruning

Based on the description of the question, we know that if s2 is a scrambled string of s1, there must be a break point which could divide s1 and s2 into s11, s12 and s21, s22. s11 is a scrambled string of s21 and s12 is a scrambled string of s22. Or s12 is a scrambled string of s22 and s12 is a scrambled string of s21.

So, now, the question is to find the break point.

One method is recursion. But it's too slow.

The other is DP. 

We define a boolean array t3[k][i][j] as whether the s1[i:i+k] is a scrambled string of s2[j:j+k] or not.

The main framework of program is:

	for k in range(2,n+1) :
		for i in range(n-k+1)[::-1] :
			for j in range(n-k+1)[::-1] :
				for h in range(1,k) :

Because the time limitation is strict in LeetCode, we need extra two pruning.

1. If the two substrings contain different letters, continue. (The answer must be false)
2. If we have found a break point for current substrings, break. (Do not need to enumerate other points)


###Code
	   
	class Solution:
		# @return a boolean
		def isScramble(self, s1, s2):
			if len(s1) != len(s2):
				return False
			n = len(s1)
			if n == 0:
				return True
			a = set(s1)
			b = set(s2)
			if a != b:
				return False
			
			t3=[[[False for i in range(n+1)] for i in range(n+1)]for i in range(n+1)]
			
			for i in range(n):
				for j in range(n):
					t3[1][i][j] = s1[i] is s2[j]

			for k in range(2,n+1) :
				for i in range(n-k+1)[::-1] :
					l1 = list(s1[i:i+k])
					l1.sort()
					for j in range(n-k+1)[::-1] :
						l2 = list(s2[j:j+k])
						l2.sort()
						if l1 != l2:
							continue
						for h in range(1,k) :
							t3[k][i][j] = t3[k][i][j] or (t3[h][i][j] and t3[k-h][i+h][j+h]) or (t3[h][i][j+k-h] and t3[k-h][i+h][j])
							if t3[k][i][j]: 
								break
			
			return t3[n][0][0]	          