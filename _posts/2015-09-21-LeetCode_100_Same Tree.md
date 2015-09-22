---
layout: post
title: LeetCode_100_Same Tree
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

###Solution
Travel the two trees together and compare the key of node at every node.

###Code
	class Solution(object):
        def isSameTree(self, p, q):
            """
            :type p: TreeNode
            :type q: TreeNode
            :rtype: bool
            """
            s1 = []
            s2 = []
            c1 = p
            c2 = q
            flag = True
            while s1 or c1 or s2 or c2:
                if c1 or c2:
                    if c1:
                        s1.append(c1)
                        c1 = c1.left
                    else:
                        flag = False
                        break                    
                    if c2:
                        s2.append(c2)
                        c2 = c2.left
                    else:
                        flag = False
                        break
                else:
                    c1 = s1.pop()
                    c2 = s2.pop()
                    if c1.val != c2.val:
                        flag = False
                        break
                    c1 = c1.right
                    c2 = c2.right

            return flag