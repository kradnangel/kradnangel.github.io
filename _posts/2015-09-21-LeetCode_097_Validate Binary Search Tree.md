---
layout: post
title: LeetCode_097_Validate Binary Search Tree
categories: [LeetCode]
tags: [LeetCode, python, tree, recursion]
fullview: true
---
###Question
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys less than the node's key.
* The right subtree of a node contains only nodes with keys greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

###Solution
I solve this question by checking every node wiht its left child and right child recursively.

In order to check a node, firstly, we need to check that the left child is less than this node and the right child is greater than this node. Except this, we need also to record the upper bound and lower bound. For example, it means that when we have checked the root and ready to check the left node of the root. The right child of the left node of the root should be greater than the left node of the root, but it should be less than the root. The key of root is the upper bound of the left subtree. In the process, the upper bound and lower bound will be update in every movement. When move to check the left child, update the upper bound with the key of current node. When move to check the right child, update the lower bound the the key of current node. 

When whole process is finished, we could get the answer.

###Code
	def check(p, upper, lower):
		ans = True
		if p.left:
			if (p.left.val < p.val):
				if (lower == -1) or (p.left.val > lower):
					ans = ans and check(p.left, p.val, lower)
				else: return False
			else: return False
		if p.right:
			if (p.right.val > p.val):
				if (upper == -1) or (p.right.val < upper):
					ans = ans and check(p.right, upper, p.val)
				else: return False
			else: return False
		return ans

	class Solution(object):
	    def isValidBST(self, root):
	        """
	        :type root: TreeNode
	        :rtype: bool
	        """
	        if root:
	        	return check(root, -1, -1)
	        else: return True