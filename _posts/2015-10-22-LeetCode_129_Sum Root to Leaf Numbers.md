---
layout: post
title: LeetCode_129_Sum Root to Leaf Numbers
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

For example,

    	1
       / \
      2   3
      
The root-to-leaf path 1->2 represents the number 12.

The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.

###Solution
Do preorder traversal.

Use a stack to record the ancestor node.

If current node have child havn't been visited, push it into ancestor node stack and check the child.

During the moving, add the value of current node in path to a number.

When reach the leaf node, add the current number to the sum. Then, divide the number by 10 and return to father node (first node in the ancestor node stack).

(Don't forget to pop the first node in the ancestor node stack)

If all children of current node have been visited, just keep return to father node. 

###Code
	class Solution(object):
        def sumNumbers(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            ans = 0
            if not root: return 0
            else: now = root.val
            p = root
            father = []
            used = []
            while p:
                if p.left and (p.left not in used):
                    father.append(p)
                    p = p.left
                    now = now * 10 + p.val
                elif p.right and (p.right not in used):
                    father.append(p)
                    p = p.right
                    now = now * 10 + p.val
                else:
                    if not p.left and not p.right:
                        ans += now
                    now /= 10
                    used.append(p)
                    if father:
                        p = father.pop()
                    else: break
            return ans