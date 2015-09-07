---
layout: post
title: LeetCode_095_Unique Binary Search Trees II
categories: [LeetCode]
tags: [LeetCode, python, tree, recursion]
fullview: true
---
###Question
Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

	   1         3     3      2      1
	    \       /     /      / \      \
	     3     2     1      1   3      2
	    /     /       \                 \
	   2     1         2                 3

return 

[[1, None, 2, None, 3], [1, None, 3, 2], [2, 1, 3], [3, 1, None, None, 2], [3, 2, None, 1]]


###Solution
We can notice that it's a binary search tree. Thereform, in the list [1, 2, 3, ... n], if we pick up a number, the numbers in the left which is smaller than this number will appear in the left subtree. Correspondingly, the numbers in the right which is larger than this number will appear in the right subtree. 

Thereform, we can enumerate the root node from 0 to n-1. Then, recursively, structure the left subtree by the numbers smaller than the root and structure the right subtree by the numbers larger than the root. Then make them together to get one possible binary search tree.

Function norm() is used to normalize the output.

###Code
	def norm(root):
		a = [root]
		ans = []
		while a:
			p = a.pop(0)
			if p == None:
				ans.append(None)
			else:
				ans.append(p.val)
				if p.left:
					a.append(p.left)
				else:
					a.append(None)
				if p.right:
					a.append(p.right)
				else:
					a.append(None)

		while ans[-1] == None:
			ans.pop()

		return ans	

	def getTree(l,r):
		ans = []
		if l >= r:
			ans.append(None)
			return ans
		if r-l == 1:
			ans.append(TreeNode(l))
			return ans
		for m in range(l,r):
			left = getTree(l,m)
			right = getTree(m+1,r)
			for i in range(len(left)):
				for j in range(len(right)):
					root = TreeNode(m)
					root.left = left[i]
					root.right = right[j]
					ans.append(root)	

		return ans


	class Solution(object):
	    def generateTrees(self, n):
	        """
	        :type n: int
	        :rtype:
	        """
	        if n == 0: return [[]]
	        ansList = getTree(1,n+1)
	        return map(lambda x:norm(x), ansList)