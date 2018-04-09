---
layout: post
title: LeetCode_084_Largest Rectangle in Histogram 
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
### Question
Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.


Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].


The largest rectangle is shown in the shaded area, which has area = 10 unit.

For example,

Given height = [2,1,5,6,2,3],

return 10.

### Solution

#### Enumerating O(n^2)
The simplest method we can come up with is enumerating every combinations. We enumerate the left bar L, and find the minimum height in range [L, rightMost]. 

	size = minimum height * current range
	
Time complexity: O(n^2)

#### O(n logn)
A improved method is that we can enumerate every int in the list. Assume that int is in the max size rectangle. So, we need to find the maximum size rectangle which include this int. So, what we do is try to find the first int "l" which is smaller that this int in its left. We do same thing to find the first smaller int in its right "r". Then the maximum size rectangle with this int is the height of this int * the range it can cover (r - l - 1).

If we just scan to find the smaller height, it will be too slow. Thereform, before we try to enumerate every height, we scan the height list from left to right to find left first smaller height of every height. Besides, we scan the height list from right to left to find right first smaller height of every height. 

In this process, we will use "leftMin" and "rightMin" to record the position of smaller height.

Take left as the example, when we try to find the left smaller height of current height, we first compare current height with the height of left one of current height. If the left one is smaller, just record the position of left one in "leftMin". If the left one is not smaller, we get the the position of the left first smaller height of left one from "leftMin" and compare it with the current height. We won't stop until we find a height is smaller than current height.

Since there is no height in the left of the first height, we insert "0" in the position "0". Similarly, we add "0" to the end of the height list.

#### Stack O(n)
For each bar, we need to know the position of first element in the left/right is smaller than this bar. we can use a stack. 

If stack is empty or the height of current bar  is larger than the top element in stac ), push it to stack. If the height of current bar is smaller than the top lement in the stack, (the index of current bar is the position of first element that smaller than the top element in the stack) pop up stack top element until currentHeight > stack top element or stack is empty. In the meantime, for each element poped up, caculate the size based on taking stack top element as the minHeight. The position of frist element in the left of this top element in the stack is the rightmost position of the element under this top element. So, we need a extre array or dictionary to record the rightmost position of each element in the stack. 

After scanning all bars in the given array, pop up all elements in the stack and calculate the size. 

return the max one. 

[ref](http://www.2cto.com/kf/201502/375392.html)

### Code

{% 622fd158a3dd252b1ed178320baed6d1 %}
        
{% gist 6f9a90c743f2800e783feb73c92dbbbb %}