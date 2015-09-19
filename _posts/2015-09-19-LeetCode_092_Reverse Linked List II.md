---
layout: post
title: LeetCode_092_Reverse Linked List II
categories: [LeetCode]
tags: [LeetCode, python, linked list]
fullview: true
---
###Question
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

Note:
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.

###Solution
This solution is based on the solution of '206 Reverse Linked List'

the program of reverse linked list is used to reverse the specified part of linked list. That's what the red part does. (See the drawing below)

![](/images/092.jpg)

Expect this, we also need to connect this part to its front and its rear. That's what the green part does.

We need to mark the last node 'f' of the front, the first node 'startUp' of the reverse part, the last node 'p' of the reverse part and the first node 'q' of the rear. Then try to connect: 'f.next = p' 'startUp.next = q'


###Code
	class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if head == None:
            return None
        p = head    
        f = head
        for i in range(m-1):
            if i == m-2:
                f = p    
            p = p.next            

        q = p.next
        startUp = p
        
        i = m
        while (p!= None) and (q != None) and (i < n):
            t = q.next
            q.next = p
            p = q
            q = t
            i += 1
        
        f.next = p
        startUp.next = q
        
        if m != 1:
            return head
        else:
            return p   