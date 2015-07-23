---
layout: post
title: LeetCode_065_Valid Number
categories: [LeetCode]
tags: [LeetCode, python, regular expression]
fullview: true
---
###Question
Validate if a given string is numeric.

Some examples:

"0" => true

" 0.1 " => true

"abc" => false

"1 a" => false

"2e10" => true

Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

###Solution
Key point: how to use regular expression

We can devide all valid numbers in two groups. One includes regular numbers and the other includes scientific notation. Then display them in regular expressions and use the regular expressions to check the string.

###Code
	import re

	class Solution:
		# @param {string} s
		# @return {boolean}
		def isNumber(self, s):
			s = s.strip()
			p1 = re.compile(r'^[+/-]?[0-9]*\.?[0-9]+$')
			p2 = re.compile(r'^[+/-]?[0-9]+\.$')

			f1 = True if p1.match(s) else False
			f2 = True if p2.match(s) else False

			p3 = re.compile(r'^[+/-]?[0-9]*\.?[0-9]+[e/E][+/-]?[0-9]+$')
			p4 = re.compile(r'^[+/-]?[0-9]+\.[e/E][+/-]?[0-9]+$')

			f3 = True if p3.match(s) else False
			f4 = True if p4.match(s) else False		
			return f1|f2|f3|f4