---
layout: post
title: LeetCode_094_Binary Tree Inorder Traversal
categories: [LeetCode]
tags: [LeetCode, python, tree, stack]
fullview: true
---
###Question
Given a binary tree, return the inorder traversal of its nodes' values.

For example:

Given binary tree {1,#,2,3},
   
	1
     \
      2
     /
    3
   
return [1,3,2].

Note: Recursive solution is trivial, could you do it iteratively?


###Solution
The recursive method is traversaling the left subtree, output the root and traversaling the right subtree.

The iterative method is similar. But, here, we will use a stack to save nodes which need to waitl.

First, we check the current node. If the node is not None, we push it to the stack and then check its left node. If the node is None, we get the first element in the stack which must be the father node of current node. Since the current node is None, we can just output the value of its father node and then check the right node of the father node.


###Code
	class Solution(object):
        def inorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            ans = []
            if (root == None):
                return ans
            stack = []
            p = root
            while stack or (p != None):
                if p:
                    stack.append(p)
                    p = p.left
                else:
                    p = stack.pop()
                    ans.append(p.val)
                    p = p.right

            return ans