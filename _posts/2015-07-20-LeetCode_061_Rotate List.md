---
layout: post
title: LeetCode_060_Rotate List
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given a list, rotate the list to the right by k places, where k is non-negative.

For example:

Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.

###Solution
First, find the length 'l' of the list and use k = l - k % l to find the new head of the list.

Second, new a point and point out the new head and new tail. 

At last, tail point to the head, head move to the new location and make the new tail have a None next.

###Code
	class Solution:
	    # @param {ListNode} head
	    # @param {integer} k
	    # @return {ListNode}
	    def rotateRight(self, head, k):
	    	if head == None:
	    		return head
	        l = 1
	        tail = head
	        while tail.next != None:
	        	l += 1
	        	tail = tail.next
	        k = l - k % l
	        p = head
	        while k > 1:
	        	k -= 1
	        	p = p.next
	        tail.next = head
	        head = p.next
	        p.next = None
	        return head