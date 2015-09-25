---
layout: post
title: LeetCode_105_LeetCode_105_Construct Binary Tree from Preorder and Inorder Traversal Traversal
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given preorder and inorder traversal of a tree, construct the binary tree.

###Solution
Recursion method will exceed the memory limitation.

So, here we use several stack to save the nodes we havn't processed. In the process, at every node, we process its left subtree first and push its right subtree to the stack to wait for processing. 

You can find detail by reading my code. I have made some comments in code.

###Code
	class Solution(object):
        def buildTree(self, preorder, inorder):
            """
            :type preorder: List[int]
            :type inorder: List[int]
            :rtype: TreeNode
            """
            if not preorder:
                return None
            # Set the root
            key = preorder[0]
            root = TreeNode(key)
            # find the location of root in the inorder list
            mid = inorder.index(key)
            # push the right subtree of root to Stack
            preStack = [preorder[mid+1:]]
            inStack = [inorder[mid+1:]]
            # The left subtree will be processed in next step
            preorder = preorder[1:mid+1]
            inorder = inorder[:mid]
            # father list is used to save the father node
            father = [root]
            # If left subtree is not empty, process it.
            # Otherwise, pop the right subtree and process it.
            while preStack or preorder:
                if preorder:
                    # connect the root of left subtree to the root
                    key = preorder[0]
                    p = TreeNode(key)
                    father[-1].left = p
                    father.append(p)                
                    # push right subtree and get left subtree of current node
                    mid = inorder.index(key)
                    preStack.append(preorder[mid+1:])
                    inStack.append(inorder[mid+1:])               
                    preorder = preorder[1:mid+1]
                    inorder = inorder[:mid]
                else:
                    # pop the right subtree
                    preorder = preStack.pop()
                    inorder = inStack.pop()
                    while father and preStack and preorder == []:
                        father.pop()
                        preorder = preStack.pop()
                        inorder = inStack.pop()
                    # If all subtree have been processed, exit
                    if preorder == []:
                        break
                    # connect the right subtree to the root
                    key = preorder[0]
                    p = TreeNode(key)
                    father[-1].right = p
                    father.pop() # pop this father node as it had two children now
                    father.append(p)
                    # push right subtree and get left subtree of current node
                    mid = inorder.index(key)
                    preStack.append(preorder[mid+1:])
                    inStack.append(inorder[mid+1:])               
                    preorder = preorder[1:mid+1]
                    inorder = inorder[:mid]

            return root