---
layout: post
title: LeetCode_101_Symmetric Tree
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:

    	1
	   / \
	  2   2
	 / \ / \
	3  4 4  3
	
But the following is not:

		1
	   / \
	  2   2
	   \   \
	   3    3

Note:

Bonus points if you could solve it both recursively and iteratively.

###Solution
I use both the inorder traversal and layer traversal to check the tree.

If it's a Symmetric Tree, its inorder traversal will be a
palindrome and every layer also will be a palindrome. So, what we need to do is to check these.

###Code
	class Solution(object):
	    def isSymmetric(self, root):
	        """
	        :type root: TreeNode
	        :rtype: bool
	        """
	        stack = []
	        p = root
	        seq = []
	        while stack or p:
	            if p:
	                stack.append(p)
	                p = p.left
	            else:
	                p = stack.pop()
	                seq.append(p.val)
	                p = p.right
	        
	        n = len(seq)
	        flag = True
	        for i in range(0, n//2):
	            if seq[i] != seq[n-i-1]:
	                flag = False
	                break

	        s = [root]
	        while root and s and flag:
	        	t = []
	        	for x in s:
	        		if x.left: t.append(x.left)
	        		if x.right: t.append(x.right)
	        	l = len(t)
	        	if l % 2 != 0:
	        		flag = False
	        		break
	        	for i in range(0, l//2):
	        		if t[i].val != t[l-i-1].val:
	        			flag = False
	        			break
	        	s = t

	        return flag