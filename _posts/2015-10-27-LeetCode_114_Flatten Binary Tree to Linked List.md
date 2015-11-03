---
layout: post
title: LeetCode_114_Flatten Binary Tree to Linked List
categories: [LeetCode]
tags: [LeetCode, python, tree]
fullview: true
---
###Question
Given a binary tree, flatten it to a linked list in-place.

For example,
Given

         1
        / \
       2   5
      / \   \
     3   4   6
     
The flattened tree should look like:

	1
     \
      2
       \
        3
         \
          4
           \
            5
             \
              6
              
###Solution
The idea is that from the root, we try to deal with every node by this way: 

If current node 'p' doesn't have left node, we just move to its right node. 

Otherwise, try to find the rightest node 'q' of left child, then connect right child of current node to this node 'q' as its right child. Then make left child of current node as right child. *AND set left child of current node as NULL.*

Repeat until current node is NULL.



###Code
	class Solution(object):
        def flatten(self, root):
            """
            :type root: TreeNode
            :rtype: void Do not return anything, modify root in-place instead.
            """
            if root:
                p = root
                while p:
                    if not p.left:
                        p = p.right
                    else:
                        q = p.left
                        while q.right:
                            q = q.right
                        q.right = p.right
                        p.right = p.left
                        p.left = None
                        p = p.right