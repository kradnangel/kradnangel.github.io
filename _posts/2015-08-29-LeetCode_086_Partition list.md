---
layout: post
title: LeetCode_086_Partition list
categories: [LeetCode]
tags: [LeetCode, python, listNode]
fullview: true
---
###Question
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.

###Solution
Just use one list to hold the smaller nodes and other one to hold the greater or euqal nodes. Then connect them.


###Code
	class Solution(object):
	    def partition(self, head, x):
	        """
	        :type head: ListNode
	        :type x: int
	        :rtype: ListNode
	        """
	        a = ListNode(0)
	        aHead = a
	        b = ListNode(0)
	        bHead = b
	        while head != None:
	        	if head.val < x:
	        		a.next = head
	        		a = a.next
	        	else:
	        		b.next = head
	        		b = b.next
	        	head = head.next
	        b.next = None
	        a.next = bHead.next
	        head = aHead.next	

	        return head