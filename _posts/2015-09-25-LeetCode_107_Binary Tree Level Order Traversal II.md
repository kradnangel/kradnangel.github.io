---
layout: post
title: LeetCode_107_Binary Tree Level Order Traversal II
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:

Given binary tree {3,9,20,#,#,15,7},

    	3
	   / \
	  9  20
	    /  \
	   15   7

return its bottom-up level order traversal as:

	[
	  [15,7],
	  [9,20],
	  [3]
	]


###Solution
Just use Level Order Traversal to solve this problem and store the level reversed.

###Code
	class Solution(object):
	    def levelOrderBottom(self, root):
	        """
	        :type root: TreeNode
	        :rtype: List[List[int]]
	        """
	        
	        s = [root]
	        ans = []
	        while s and root:
	        	t = []
	        	for p in s:
	        		if p.left: t.append(p.left)
	        		if p.right: t.append(p.right)
	        	ans.insert(0,map(lambda x:x.val, s))
	        	s = t

	        return ans