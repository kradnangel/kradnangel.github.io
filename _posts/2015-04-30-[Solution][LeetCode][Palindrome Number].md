---
layout: post
title: [Solution][LeetCode][Palindrome Number]
categories: [fsharp]
tags: [fsharp, random, array]
fullview: true
---
###Question
Determine whether an integer is a palindrome. Do this without extra space.

Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.


###Solution
Pick up and compare the first number and last number of the integer.

Then look at the second and penult.

...

There are some details in this question.

You should check every number instead of just subtracting the corresponding numbers which are checked from the integer and checking the remainder.

For example, when you're checking the first number and last number of 100021, if you just use 100021 - 100000 - 1, you will get 2. In this case, your program will return true, which makes the mistake.


###Code
	class Solution:
		# @return a boolean
		def isPalindrome(self, x):
			if x < 0:
				return False
	    
			k = 1
			while k * 10 <= x:
				k *= 10
		
			while (k > 0) and (x % 10 == x // k) :
				x -= x // k * k
				x //= 10
				k //= 100

			if k == 0:
				return True
			else:
				return False
