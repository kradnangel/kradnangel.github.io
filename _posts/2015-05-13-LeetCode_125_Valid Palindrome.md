---
layout: post
title: LeetCode_125_Valid Palindrome
categories: [LeetCode]
tags: [LeetCode, python, String]
fullview: true
---
###Question
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

###Solution
This question is about string manipulation.

Firstly, use string.lower() to convert all letters to lowercase letters. 

Secondly, remove all other symbols, including punctuation.

Finally, simultaneously, starting at header and tail, compare the letters.



###Code
	class Solution:
		# @param s, a string
		# @return a boolean
		def isPalindrome(self, s):
			s = s.lower()
			fomart = 'abcdefghijklmnopqrstuvwxyz0123456789'   
			for c in s:
				if not c in fomart:   
					s = s.replace(c,'');
			l = len(s)
			if l == 0: return True
			i = 0
			while i <= l/2 :
				if s[i] != s[l-i-1]:
					return False
				i += 1
			return True