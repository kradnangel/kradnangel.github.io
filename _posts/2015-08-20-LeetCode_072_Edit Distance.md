---
layout: post
title: LeetCode_072_Edit Distance
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

a) Insert a character
b) Delete a character
c) Replace a character

###Solution
DP.

We set a[i][j] as the distance of converting word1[0:i-1] to word2[0:j-1].

There are three ways to get a[i][j]:

1. a[i-1][j] + 1, which means deleting a character
2. a[i][j-1] + 1, which means adding a character
3. a[i-1][j-1] + (word1[i-1] != word2[j-1]), which means replace a character

We choose the minimum number of these three as the answer of a[i][j].

a[len(word1) - 1][len(word2) - 1] is the final answer.

[Reference](http://www.cnblogs.com/lihaozy/archive/2012/12/31/2840152.html)

###Code
	class Solution:
		# @param {string} word1
		# @param {string} word2
		# @return {integer}
		def minDistance(self, word1, word2):
			l1 = len(word1)+1
			l2 = len(word2)+1
			a = [[0 for j in range(l2)] for i in range(l1)]

			for i in range(l1):
				a[i][0] = i
			for j in range(l2):
				a[0][j] = j

			for i in range(1, l1):
				for j in range(1, l2):
					a[i][j] = min(a[i-1][j]+1, a[i][j-1]+1, a[i-1][j-1] + (word1[i-1] != word2[j-1]))

			return a[l1-1][l2-1]