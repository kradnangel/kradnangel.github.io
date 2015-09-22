---
layout: post
title: LeetCode_104_Maximum Depth of Binary Tree Traversal
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

###Solution
Here I use inorder traversal to solve the problem. In the traversal, use a depth list to record the depth of every node. Use 'depthMax' to record the max depth.


###Code
	class Solution(object):
	    def maxDepth(self, root):
	        """
	        :type root: TreeNode
	        :rtype: int
	        """
	        p = root
	        stack = []
	        depth = []
	        depthNow = 0
	        depthMax = 0
	        while stack or p:
	        	if p:
	        		stack.append(p)
	        		p = p.left
	        		depthNow += 1
	        		depth.append(depthNow)
	        		depthMax = depthNow if depthNow > depthMax else depthMax
	        	else:
	        		p = stack.pop()
	        		depthNow = depth.pop()
	        		p = p.right

	        return depthMax