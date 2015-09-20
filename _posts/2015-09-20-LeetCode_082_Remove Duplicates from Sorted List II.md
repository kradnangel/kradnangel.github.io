---
layout: post
title: LeetCode_082_Remove Duplicates from Sorted List II
categories: [LeetCode]
tags: [LeetCode, python, linked list]
fullview: true
---
###Question
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,

Given 1->2->3->3->4->4->5, return 1->2->5.

Given 1->1->1->2->3, return 2->3.

###Solution
This question differ with "Remove Duplicates from Sorted List" on that we need to leave only distinct numbers. It means that if a number has duplicate(s), we need to throw these numbers away.

So, in this case, based on the idea of program of "Remove Duplicates from Sorted List", we need one more point 'front' which is used to mark the front node of current node. Because there is no node before the head node, we new a node 'beforeHead' and link it before head node.

In the process, if the next node 'q' is different with 'p', we just move every pointers one step forward. If they are the same, we keep moving 'q' forward till they are different. Then link the 'front' and 'q'. That is 'front.next = q'. It means that we throw the nodes which have dupilicate(s). Then make 'p = q' to check the next node.

At last, return the next node of 'beforeHead'.

###Code
	class Solution(object):
        def deleteDuplicates(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            front = ListNode(0)
            front.next = head
            beforeHead = front
            p = head
            while p != None:
                flag = False            
                q = p.next
                while q != None:
                    if q.val == p.val:
                        q = q.next
                        flag = True
                    else: break
                
                if flag:
                    front.next = q
                else:
                    front = p
                p = q

            return beforeHead.next