---
layout: post
title: LeetCode_089_Gray Code
categories: [LeetCode]
tags: [LeetCode, python, code]
fullview: true
---
###Question
The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:

	00 - 0
	01 - 1
	11 - 3
	10 - 2

Note:
For a given n, a gray code sequence is not uniquely defined.

For example, [0,2,3,1] is also a valid gray code sequence according to the above definition.

For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.

###Solution
Just start at 0. Then change the bit from tail. Every time, start at tail and change the bit. If the new code already exist, recover the bit, change the bit before current bit and check the new code again till we find a real new code.


###Code
	class Solution(object):
	    def grayCode(self, n):
	        """
	        :type n: int
	        :rtype: List[int]
	        """
	        a = [0 for i in range(n)]
	        done = [list(a)]
	        i = 1
	        m = 2**n
	        while i < m:
	            j = n - 1
	            a[j] = 1 - a[j]    
	            while (j >= 0) and (a in done):
	                a[j] = 1 - a[j]
	                j -= 1
	                a[j] = 1 - a[j]
	            done.append(list(a))
	            i += 1

	        ans = []

	        for x in done:
	            k = 0
	            for j in range(n-1, -1, -1):
	                k += x[j] * 2**(n-j-1)                
	            ans.append(int(k))

	        return ans