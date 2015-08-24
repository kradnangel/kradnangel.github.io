---
layout: post
title: LeetCode_076_Minimum Window Substring
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".

Note:
If there is no such window in S that covers all characters in T, return the emtpy string "".

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

###Solution
A point may be mis is that the characters in T could be repeated.

The main idea is that we will maintain a list "current" which is used to hold the satisfactory substring and a list "location" which is used to record the location of every characters of list "current" in the string "s".

We will scan the "s" once. In the process, if we meet a char which appears in t, we will add it to the "current" and add its location to "location". If it has been in "current", we will update the location info of this char.

In whole process, if "current" has covered all characters in T, we will calculate the length of the substring "current". If the new length is smaller, we update the answer length. Here, we use 'left' and 'right' mark the start position and end position of substring in the string "s".

###Code
	class Solution(object):
		def minWindow(self, s, t):
			"""
			:type s: str
			:type t: str
			:rtype: str
			"""
			
		   	ls = len(s)
		   	lt = len(t)

		   	left = 0
		   	right = ls
		   	current = []
		   	location = []
		   	toFind = list(t)

		   	for i in range(ls):
		   		if s[i] in toFind:	# Find the first location of every char
		   			current.append(s[i])
		   			location.append(i)
		   			toFind.pop(toFind.index(s[i]))
		   		elif s[i] in t:		# Update the locatio of every char
		   			oldOne = current.index(s[i])
		   			current.pop(oldOne)
		   			location.pop(oldOne)
		   			current.append(s[i])
		   			location.append(i)
		   		if toFind == []:	# Calc the length of the substring
		   			if location[-1] - location[0] < right - left:
		   				left = location[0]
		   				right = location[-1]	   			

		   	if right - left != ls:
		   		ans = s[left:right+1]
		   	else:
		   		ans = ""
		   	return ans