---
layout: post
title: LeetCode_103_Binary Tree Zigzag Level Order Traversal
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:

Given binary tree {3,9,20,#,#,15,7},

	    3
	   / \
	  9  20
	    /  \
	   15   7

return its zigzag level order traversal as:
	
	[
	  [3],
	  [20,9],
	  [15,7]
	]

###Solution
Just use the layer order traversal to solve it. When traveling, I use a 'direct' to indicate this layer should be added in order or in reverse order. Here I use 'map' function to shorten the code.

###Code
	class Solution(object):
	    def zigzagLevelOrder(self, root):
	        """
	        :type root: TreeNode
	        :rtype: List[List[int]]
	        """
	        s = [root]
	        ans = []
	        direct = 1
	        while s and root:
	        	t = []
	        	ans.append(map(lambda x:x.val, s[::direct]))
	        	for x in s:
	        		if x.left: t.append(x.left)
	        		if x.right: t.append(x.right)
	        	s = t
	        	direct = -direct

	        return ans