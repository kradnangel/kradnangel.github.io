---
layout: post
title: LeetCode_084_Largest Rectangle in Histogram 
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.


Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].


The largest rectangle is shown in the shaded area, which has area = 10 unit.

For example,

Given height = [2,1,5,6,2,3],

return 10.

###Solution
The easiest method we can come up with is enumerating every combinations. However, it is too slow.

A improved method is that we can enumerate every int in the list. Assume that int is in the max size rectangle. So, we need to find the maximum size rectangle which include this int. So, what we do is try to find the first int "l" which is smaller that this int in its left. We do same thing to find the first smaller int in its right "r". Then the maximum size rectangle with this int is the height of this int * the range it can cover (r - l - 1).

If we just scan to find the smaller height, it will be too slow. Thereform, before we try to enumerate every height, we scan the height list from left to right to find left first smaller height of every height. Besides, we scan the height list from right to left to find right first smaller height of every height. 

In this process, we will use "leftMin" and "rightMin" to record the position of smaller height.

Take left as the example, when we try to find the left smaller height of current height, we first compare current height with the height of left one of current height. If the left one is smaller, just record the position of left one in "leftMin". If the left one is not smaller, we get the the position of the left first smaller height of left one from "leftMin" and compare it with the current height. We won't stop until we find a height is smaller than current height.

Since there is no height in the left of the first height, we insert "0" in the position "0". Similarly, we add "0" to the end of the height list.

A better [algorithm](http://www.2cto.com/kf/201502/375392.html) using stack (in Chinese).

###Code
	class Solution(object):
    def largestRectangleArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        maxSize = 0
        height.insert(0,-1)
        n = len(height)
        leftMin = [0]
        for i in range(1, n):
            if height[i - 1] < height[i]:
                leftMin.append(i - 1)
            else:
                j = leftMin[i - 1]
                while height[j] >= height[i]:
                    j = leftMin[j]
                leftMin.append(j)
        leftMin.append(7)

        height.append(-1)
        n = len(height)
        rightMin = [n-1]
        for i in range(n - 2, 0, -1):
            if height[i + 1] < height[i]:
                rightMin.append(i + 1)
            else:
                j = rightMin[n - (i+2)]
                while height[j] >= height[i]:
                    j = rightMin[n - (j+1)]
                rightMin.append(j)    
        rightMin.append(0)          
        rightMin.reverse()
        for i in range(1, n-1):
            l = i - 1
            r = i + 1
            while (l >= 0):
                if (height[l] >= height[i]): l = leftMin[l]
            	else: break
            while (r < n):
                if (height[r] >= height[i]): r = rightMin[r]
            	else: break
            size = (r - l - 1) * height[i]
            if size > maxSize:
                maxSize = size

        return maxSize