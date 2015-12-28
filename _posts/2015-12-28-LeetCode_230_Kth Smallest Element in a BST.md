---
layout: post
title: LeetCode_230_Kth Smallest Element in a BST
categories: [LeetCode]
tags: [LeetCode, python, tree]
fullview: true
---
###[Question](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note:

You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Follow up:

What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?
       
### Solution
The solution is quite straightforward -- in-order travrsal. Stop and return the value when the kth node is visited. 

For follow-up:
   
The idea is add a attribute to tree node -- rank. The rank of node is the sum of the size of left subtree plus one which equals the order of this node in the tree with this node as the root. 

So, when trying to find the kth node, check the rank of root first, if it is larger than k, go left. If it is smaller than k, go right and k minus the rank of the root. Then repeat.          
           
### Code
	class Solution(object):
	    def kthSmallest(self, root, k):
	        """
	        :type root: TreeNode
	        :type k: int
	        :rtype: int
	        """
	        p = root
	        stack = []
	        while k and (stack or p):
	            if p:
	                stack.append(p)
	                p = p.left
	            else:
	                p = stack.pop()
	                ans = p.val
	                p = p.right
	                k -= 1
	
	        return ans
                    