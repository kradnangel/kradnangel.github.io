---
layout: post
title: LeetCode_113_Path Sum II
categories: [LeetCode]
tags: [LeetCode, python, tree]
fullview: true
---
###Question
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:

Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

return

	[
		[5,4,11,2],
	    [5,8,4,5]
	]     
    
    
###Solution
There are some key points here. 

1. The value can be repeated.
2. The value can be negative.

So, we need to search whole tree instead of doing some pruning.

So, we can just do post-order traversal to solve this question. If current node isn't leaf, check its children. Otherwise, check the sum. Here I use a dict for every node to record the values of nodes in its path to root. 


###Code
	class Solution(object):
        def pathSum(self, root, sums):
            """
            :type root: TreeNode
            :type sum: int
            :rtype: List[List[int]]
            """
            ans = []
            if not root: return []
            d = {}
            d[root] = [root.val]
            stack = [root]
            while stack:
                p = stack.pop()
                if p.left: 
                    stack.append(p.left)
                    d[p.left] = d[p]+[p.left.val]
                if p.right:
                    stack.append(p.right)
                    d[p.right] = d[p]+[p.right.val]
                if not p.left and not p.right:
                    if sum(d[p]) == sums:
                        ans.append(d[p])
            return ans