---
layout: post
title: LeetCode_116_Populating Next Right Pointers in Each Node
categories: [LeetCode]
tags: [LeetCode, python, tree]
fullview: true
---
###Question
Given a binary tree

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
    
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

Note:

You may only use constant extra space.

You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

For example,

Given the following perfect binary tree,

         1
       /  \
      2    3
     / \  / \
    4  5  6  7
    
After calling your function, the tree should look like:

         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL              
    
    
###Solution
Just traverse the tree in layer order. Use one list to record the current layer nodes, another to record the next layer nodes. In every layer, connect the nodes.

###Code
	class Solution(object):
        def connect(self, root):
            """
            :type root: TreeLinkNode
            :rtype: nothing
            """
            if root:
                s1 = [root]
                s2 = []
                while s1:
                    for i in range(len(s1)-1):
                        s1[i].next = s1[i+1]
                    for x in s1:
                        if x.left: s2.append(x.left); print x.left.val
                        if x.right: s2.append(x.right); print x.right.val
                    s1 = s2
                    s2 = []