---
layout: post
title: LeetCode_060_Permutation Sequence
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"

Given n and k, return the kth permutation sequence.

Note: Given n will be between 1 and 9 inclusive.

###Solution
We need to calculate every number in every position directly. 

Take n = 4 and k = 13 as an example.

Start at the first location, we have 4 candidates numbers = [1,2,3,4]. In the first location, the 24 sequences will start at 1 or 2 or 3 or 4. And the first 6 sequences will start at 1 and the following 6 sequences will start at 2 and so on.

Why is 6? Because there are 3 numbers after the first location. There are 6 kind of permutation Sequences.

So, in order to find the right number in the first location of sequence, (13 - 1) / 6 = 2. So it should be numbers[2] = 3. Why we should minus 1 before division? Because 

1-6   : 1

7-12  : 2

13-18 : 3

19-24 : 4

If the k = 6, the answer should be 1432.

After we get the number which should appear in the first location, we can do the same thing to get the following numbers. 

###Code
	class Solution:
	    # @param {integer} n
	    # @param {integer} k
	    # @return {string}
	    def getPermutation(self, n, k):
	    	upper = [1]
	    	p = 1
	    	for i in range(1,n+1):
	    		upper.append(upper[i-1] * i)
	    	numbers = range(1,n+1)
	    	s = ''
	    	for i in range(n,0,-1):
	    		p = (k-1) / upper[i-1]
	    		if p*upper[i-1] != k:
	    			k -= p * upper[i-1]
	    		print k,p,numbers,upper[i-1]
	    		s += str(numbers[p])
	    		numbers.pop(p)
	    	return s