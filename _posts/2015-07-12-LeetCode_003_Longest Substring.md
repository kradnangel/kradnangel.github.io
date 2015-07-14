---
layout: post
title: LeetCode_003_Longest Substring
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

###Solution
First, use a list to hold the longest substring and use a  set to hold the same substring. The set is used to check a char is in the substring or not easily.

Second, we start at the first char of the string, if this char is not in the substring, we add it to the tail of the substring. If it is in the substring, we have to remove the char from the head of the substring until we have removed the same char as the char we need to add to the tail of substring. Then add the new char to the tail of substring. Repeat above steps to deal with the whole string. In this process, we will record the length of the current substring. The max length is the answer.

Last, return the answer.


###Code
	class Solution:
		# @param {string} s
		# @return {integer}
		def lengthOfLongestSubstring(self, s):
			ans = 0
			length = 0
			longest = []
			ansset = set([])
			for x in s:
				if x in ansset:
					while (length > 0) & (longest[0] != x):
							ansset.remove(longest[0])
							longest.pop(0)
							length -= 1
					if length > 0:
						ansset.remove(longest[0])
						longest.pop(0)
						length -= 1
				
				ansset.add(x)
				longest.append(x)
				length += 1
				if length > ans:
						ans = length
				
			return ans