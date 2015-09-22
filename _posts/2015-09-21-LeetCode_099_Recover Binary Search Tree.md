---
layout: post
title: LeetCode_099_Recover Binary Search Tree
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

###Solution
The main idea is using the inorder traversal to get the order and find the numbers which is in wrong order.

Here I just use a list 'q' which is size in 4 to contain the sequence. The feature of wrong order number is that it's larger than front one or it's smaller than rear one and if we delete this number, the front one will smaller than the rear one (the order recovers).

Don't forget to check the first number and last number.

At last, swap the two wrong order numbers.

###Code
	class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        stack = []
        p = root
        q = []
        s = []
        while stack or p:
            if p:
                stack.append(p)
                p = p.left
            else:
                p = stack.pop()
                q.append(p)
                if len(q) > 3:
                    q.pop(0)
                if len(q) == 3:
                    if not((q[1].val < q[2].val) and (q[1].val > q[0].val)):
                        if q[0].val < q[2].val:
                            s.append(q[1])
                elif len(q) == 2:
                    if q[0].val > q[1].val:
                        s.append(q[0])
                
                p = p.right
        if len(q) >= 2:        
            if q[-1].val < q[-2].val:
                s.append(q[-1])

        if len(s) == 2:
            t = s[0].val
            s[0].val = s[1].val
            s[1].val = t