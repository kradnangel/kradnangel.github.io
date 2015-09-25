---
layout: post
title: LeetCode_106_Construct Binary Tree from Inorder and Postorder Traversal
categories: [LeetCode]
tags: [LeetCode, python, tree, traversal]
fullview: true
---
###Question
Given inorder and postorder traversal of a tree, construct the binary tree.

###Solution
The same idea with 'Construct Binary Tree from Preorder and Inorder Traversal'.

We use several stacks to save the nodes we havn't processed. In the process, at every node, we new current node first, then process its left subtree and push its right subtree to the stack to wait for processing later. 

You can find detail by reading my code. I have made some comments in code.

###Code
	class Solution(object):
	    def buildTree(self, inorder, postorder):
	        """
	        :type postorder: List[int]
	        :type inorder: List[int]
	        :rtype: TreeNode
	        """
	        if not postorder:
	            return None
	        # Set the root
	        key = postorder[-1]
	        root = TreeNode(key)
	        # find the location of root in the inorder list
	        mid = inorder.index(key)
	        # push the right subtree of root to Stack
	        postStack = [postorder[mid:-1]]
	        inStack = [inorder[mid+1:]]
	        # The left subtree will be processed in next step
	        postorder = postorder[:mid]
	        inorder = inorder[:mid]
	        # father list is used to save the father node
	        father = [root]
	        # If left subtree is not empty, process it.
	        # Otherwise, pop the right subtree and process it.
	        while postStack or postorder:
	            if postorder:
	                # connect the root of left subtree to the root
	                key = postorder[-1]
	                p = TreeNode(key)
	                father[-1].left = p
	                father.append(p)                
	                # push right subtree and get left subtree of current node
	                mid = inorder.index(key)
	                postStack.append(postorder[mid:-1])
	                inStack.append(inorder[mid+1:])               
	                postorder = postorder[:mid]
	                inorder = inorder[:mid]
	            else:
	                # pop the right subtree
	                postorder = postStack.pop()
	                inorder = inStack.pop()
	                while father and postStack and postorder == []:
	                    father.pop()
	                    postorder = postStack.pop()
	                    inorder = inStack.pop()
	                # If all subtree have been processed, exit
	                if postorder == []:
	                    break
	                # connect the right subtree to the root
	                key = postorder[-1]
	                p = TreeNode(key)
	                father[-1].right = p
	                father.pop() # pop this father node as it had two children now
	                father.append(p)
	                # push right subtree and get left subtree of current node
	                mid = inorder.index(key)
	                postStack.append(postorder[mid:-1])
	                inStack.append(inorder[mid+1:])               
	                postorder = postorder[:mid]
	                inorder = inorder[:mid]

	        return root