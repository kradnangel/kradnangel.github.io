---
layout: post
title: LeetCode_276_Paint Fence
categories: [LeetCode]
tags: [LeetCode, python, DP]
fullview: true
---
###[Question](https://leetcode.com/problems/paint-fence/)
There is a fence with n posts, each post can be painted with one of the k colors.

You have to paint all the posts such that no more than two adjacent fence posts have the same color.

Return the total number of ways you can paint the fence.

Note:
n and k are non-negative integers
	
### Solution
There are two cases:

1. The last two posts are different colors. For total number of ways (n-1) posts could be painted, there are k-1 ways to paint the last one post.
2. The last two posts are the same color. For total number of ways (n-2) posts could be painted, there are k-1 ways to paint the last two posts.

### Code
	class Solution(object):
        def numWays(self, n, k):
            """
            :type n: int
            :type k: int
            :rtype: int
            """
            a = [0 for i in xrange(n+3)]
            a[0] = 0
            a[1] = k
            a[2] = k**2
            for i in xrange(3,n+1):
                a[i] = (k-1)*(a[i-2]+a[i-1])
            return a[n]