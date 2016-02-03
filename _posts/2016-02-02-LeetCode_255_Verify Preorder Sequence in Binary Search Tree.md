---
layout: post
title: LeetCode_255 Verify Preorder Sequence in Binary Search Tree
categories: [LeetCode]
tags: [LeetCode, python, DP]
fullview: true
---
### [Question](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/)
Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

You may assume each number in the sequence is unique.

Follow up:

Could you do it using only constant space complexity?

### Solution
First of all, we should think this question from the aspect of pre-order (root, left, right).

Secondly, this is an binary search tree. So, the left child smaller than root node. The root node is smaller than right child.

(Noticed that, each number in the sequence is unique)

So, we need a stack to simulate the traversal. 

If current node is smaller than top of stack, it means that this node is on the left of the node of top of stack, which also means that we are going left. 

If current node is larger than the node of top of stack, it means that this is a right node. 

But, the question is which node in the stack is the father node of current node? -- We keep popping until we find a node is larger than current node, this must be the father node of its father node and its father node is just popped out.

Why we need to pop out the father node of this current node? -- Because its the current lower bound. So that we will have a lower bound to check whether the input sequence is valid. Also, It will be updated while the program scans. Another reason is that the pre-order is ‘root, left, right’. So, after popping out the father node of current node, the root and left part of this subtree are all popped out of stack. (We are using stack to simulate the traversal)


### Code
{% gist b2e7077901ed5dea8421 %}          