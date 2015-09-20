---
layout: post
title: LeetCode_083_Remove Duplicates from Sorted List
categories: [LeetCode]
tags: [LeetCode, python, linked list]
fullview: true
---
###Question
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,

Given 1->1->2, return 1->2.

Given 1->1->2->3->3, return 1->2->3.

###Solution
Use a pointer 'p' to point the current node and use another pointer 'q' to point the next node.

If 'q.val == p.val', then make 'q' point the next node and compare again. Repeat until they are not equal.

Then we can just make 'p.next = q'. In this way, we throw the duplicates away.

###Code
	class Solution(object):
	    def deleteDuplicates(self, head):
	        """
	        :type head: ListNode
	        :rtype: ListNode
	        """
	        p = head
	        while p != None:
	        	# now = p.val
	        	q = p.next
	        	while q != None:
	        		if q.val == p.val:
		        		q = q.next
		        	else: break
	        	p.next = q
	        	p = q

	        return head

