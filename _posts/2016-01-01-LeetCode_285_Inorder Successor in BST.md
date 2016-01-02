---
layout: post
title: LeetCode_285_Inorder Successor in BST
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###[Question](https://leetcode.com/problems/inorder-successor-in-bst/)
Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Note: 

If the given node has no in-order successor in the tree, return null.

### Solution
Inorder traversal.

When meet the target node, mark and output next node.
           
### Code
{% highlight Python %}

	class Solution(object):
        def inorderSuccessor(self, root, p):
            """
            :type root: TreeNode
            :type p: TreeNode
            :rtype: TreeNode
            """
            stack = []
            q = root
            flag = False
            while q or stack:
                if q:
                    stack.append(q)
                    q = q.left
                else:
                    q = stack.pop()
                    if flag: return q
                    if q == p: flag = True
                    q = q.right
            return False
{% endhighlight %}            