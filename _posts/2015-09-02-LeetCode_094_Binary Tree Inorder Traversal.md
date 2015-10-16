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

The iterative method is similar. But, here, we will use a stack to save nodes which need to wait to be visited.

First, we check the current node:

-	If the node is existed, we push it in stack and check its left node. Repeat.

-	If the node is None, we pop the first node in the stack which is father node or ancestor node of current None (The left subtree of this node all have been visited). Then, output the value of this node and then check the right node of the this node. Repeat.

Stop till the stack is empty.

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