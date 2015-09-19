---
layout: post
title: LeetCode_206_Reverse Linked List
categories: [LeetCode]
tags: [LeetCode, python, linked list]
fullview: true
---
###Question
Reverse a singly linked list.

###Solution
We use three pointers, p, q, t. p points a node, q points the next node and t points the next next node. That is 'q = p.next' 't = q.next'

p and q point the two nodes which need to be switch. So, every time, 'q.next = p'

t is used to mark next node needed to be switched. So, after every switching, 'p = q' 'q = t'.


###Code
	class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
        	return None
        p = head
        q = p.next
        p.next = None
        while (p!= None) and (q != None):
            t = q.next
            q.next = p
            p = q
            q = t
       
        return p