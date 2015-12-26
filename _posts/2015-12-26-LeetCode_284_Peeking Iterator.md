---
layout: post
title: LeetCode_284_Peeking Iterator
categories: [LeetCode]
tags: [LeetCode, python, Class]
fullview: true
---
###[Question](https://leetcode.com/problems/peeking-iterator/)
Given an Iterator class interface with methods: next() and hasNext(), design and implement a PeekingIterator that support the peek() operation -- it essentially peek() at the element that will be returned by the next call to next().

Here is an example. Assume that the iterator is initialized to the beginning of the list: [1, 2, 3].

Call next() gets you 1, the first element in the list.

Now you call peek() and it returns 2, the next element. Calling next() after that still return 2.

You call next() the final time and it returns 3, the last element. Calling hasNext() after that should return false.
	
### Solution
The key point is holding the next value in advance.

### Code
	class PeekingIterator(object):
	    def __init__(self, iterator):
	        """
	        Initialize your data structure here.
	        :type iterator: Iterator
	        """
	        self.iter = iterator
	        self.p = self.iter.next() if self.iter.hasNext() else None
	
	    def peek(self):
	        """
	        Returns the next element in the iteration without advancing the iterator.
	        :rtype: int
	        """
	        return self.p
	
	    def next(self):
	        """
	        :rtype: int
	        """
	        nextOne = self.p
	        self.p = self.iter.next() if self.iter.hasNext() else None
	        return nextOne
	
	    def hasNext(self):
	        """
	        :rtype: bool
	        """
	        return self.p != None
		