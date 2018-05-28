---
layout: post
title: LeetCode_218_The Skyline Problem
categories: [LeetCode]
tags: [LeetCode, python, heap, sort]
fullview: true
---
### [Question](https://leetcode.com/problems/the-skyline-problem/description/)

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are given the locations and height of all the buildings as shown on a cityscape photo (Figure A), write a program to output the skyline formed by these buildings collectively (Figure B).

(click the link for details)

### Solution

	O(nlogn) = sort {top left and top right, O(nlogn)}  + heap {maintain highest point, O(nlogn) }

Think about scanning from left to right, all key points happen on when a building enter or exit. 

So, get all points and sort them, then scan from left to right. Use a heap to maintain the current overlapping buildings (sort by height). 

1. when a new building enter (meet a top left point),  push it to heap and check whether it's the new highest building. 

2. when a building exist (meet a top right point), lazy delete it from heap. Then check the top element in heap (highest building) is still here or not. If not, remove it and mark new top as the key point. 

trick: 

1. make -height for top left point, height for top right point to tell different AND make sure the new building enter first before old building exit (in case of two bulding have overlap in boundary)
2. -height in heap to make it max heap (python)

### Code
{% gist 382588755a79b417537bdff10bb9bae7 %}          

