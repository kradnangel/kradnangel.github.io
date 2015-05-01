---
layout: post
title: LeetCode_Valid Parentheses
categories: [LeetCode]
tags: [LeetCode, python]
fullview: true
---
###Question
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

###Solution
Use a list as a stack.

If it's a left parenthese, push.

If it's a right parenthese, pop and compare.

Finally, check the stack is empty or not.

###Code
	class Solution:
		# @return a boolean
		def isValid(self, s):
			p = []
			l = ['(','[','{']
			r = [')',']','}']
			for c in s:
				if c in l:
					p.append(c)
				elif c in r:
					if p == []:
						return False
					if p.pop() != l[r.index(c)]:
						return False
			if p == []:
				return True
			else:
				return False