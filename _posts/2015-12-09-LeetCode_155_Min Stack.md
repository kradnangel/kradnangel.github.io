---
layout: post
title: LeetCode_155_Min Stack
categories: [LeetCode]
tags: [LeetCode, python, stack]
fullview: true
---
###[Question](https://leetcode.com/problems/min-stack/)
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push(x) -- Push element x onto stack.

* pop() -- Removes the element on top of the stack.

* top() -- Get the top element.

* getMin() -- Retrieve the minimum element in the stack.


###Solution
Key idea is using a stack to store the minimun value for each position in range of [:current position + 1]

E.g.

Stack: 7 8 9 3 4 6 5 1

Min V: 7 7 7 3 3 3 3 1


###Code
	class MinStack(object):
        def __init__(self):
            """
            initialize your data structure here.
            """
            self.stack = []
            self.minv = []

        def push(self, x):
            """
            :type x: int
            :rtype: nothing
            """
            self.minv.append(x if (len(self.minv) == 0) or (x < self.minv[-1]) else self.minv[-1])
            self.stack.append(x)

        def pop(self):
            """
            :rtype: nothing
            """
            self.minv.pop()
            return self.stack.pop()

        def top(self):
            """
            :rtype: int
            """
            return self.stack[-1]

        def getMin(self):
            """
            :rtype: int
            """
            return self.minv[-1]