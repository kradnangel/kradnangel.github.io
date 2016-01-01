---
layout: post
title: LeetCode_298_Binary Tree Longest Consecutive Sequence
categories: [LeetCode]
tags: [LeetCode, python, tree, DP]
fullview: true
---
###[Question](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/)
Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

For example,

	   1
	    \
	     3
	    / \
	   2   4
	        \
	         5

Longest consecutive sequence path is 3-4-5, so return 3.

	   2
	    \
	     3
	    / 
	   2    
	  / 
	 1

Longest consecutive sequence path is 2-3,not 3-2-1, so return 2.

### Solution
Tree DP. 

From root to leaves.       

The idea is to calculate the length of Longest consecutive sequence for each node. For each node, if the difference between its value and the value of its father is 1, the length of Longest consecutive sequence of current node is the length of Longest consecutive sequence of its father plus one. Otherwise, the length of Longest consecutive sequence of current node is 1. 

So, we do it layer by layer, from root to leaves. We use a hash map (dict in python) to record the length of Longest consecutive sequence for each node. or if we can modify the structure of TreeNode, we can add one more field to record the the length of Longest consecutive sequence for each node. 
           
### Code
	class Solution(object):
	       def longestConsecutive(self, root):
	           """
	           :type root: TreeNode
	           :rtype: int
	           """
	           if not root: return 0
	           s = [root]
	           d = {root:1}
	           while s:
	               t = []
	               for p in s:
	                   if p.left: 
	                       t.append(p.left)
	                       d[p.left] = d[p] + 1 if p.left.val - p.val == 1 else 1
	                   if p.right: 
	                       t.append(p.right)
	                       d[p.right] = d[p] + 1 if p.right.val - p.val == 1 else 1
	               s = t
	
	           return max(d.values())       
 