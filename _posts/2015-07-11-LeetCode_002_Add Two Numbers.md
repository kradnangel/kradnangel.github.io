---
layout: post
title: LeetCode_002_Add Two Numbers
categories: [LeetCode]
tags: [LeetCode, python, linked]
fullview: true
---
###Question
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8

###Solution
First, new a linked list as the result linked list. New a node used to point the tail of the result linked list.

Second, add the two number from the low order(from the head). Use 'carry' to save the carry.

Last, if there is a carry in the highest order, new a node to save the carry.

<br/>

Key point of this question: how to use the ListNode and how to use new node.

###Code
	class Solution:
		# @param {ListNode} l1
		# @param {ListNode} l2
		# @return {ListNode}
		def addTwoNumbers(self, l1, l2):
			carry = 0
			tail = ListNode(0)
			ans = tail
			while (l1 != None) | (l2 != None):
				x = 0
				if l1 != None:
					x = l1.val
					l1 = l1.next
				y = 0
				if l2 != None:
					y = l2.val
					l2 = l2.next
				z = x + y + carry
				carry = z / 10
				z = z % 10
				tail.next = ListNode(z)
				tail = tail.next

			if carry > 0:
				tail.next = ListNode(carry)

			return ans.next