---
layout: post
title: LeetCode_295_Find Median from Data Stream
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###[Question](https://leetcode.com/problems/find-median-from-data-stream/)
Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 

[2,3,4] , the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Design a data structure that supports the following two operations:

void addNum(int num) - Add a integer number from the data stream to the data structure.

double findMedian() - Return the median of all elements so far.

For example:

	add(1)
	add(2)
	findMedian() -> 1.5
	add(3) 
	findMedian() -> 2

    
###Solution
The key idea of this question is using a max-heap and a min-heap to hold the median on the top. 

There are two steps that we need to do when 'addNum'. 

1. Insert the number to the heaps
2. adjust the size of heaps. 

The numbers that samller than median will been put in max-heap and the numbers that larger than median will been put in min-heap. 

After inserting, we need to adjust the size of two heaps to keep the difference of size of two heaps within 1. In order to simplify the algorithm, I keep the size of max-heap is equal to min-heap or larger 1 than min-heap. So, when the total size is odd, the median is the top of max-heap and when the total size is even, the median is the half sum of top of max-heap and top of min-heap.


###Code
	import heapq
    class MedianFinder:
        def __init__(self):
            """
            Initialize your data structure here.
            """
            self.left = []
            self.right = []
            self.l = 0
            self.r = 0

        def addNum(self, num):
            """
            Adds a num into the data structure.
            :type num: int
            :rtype: void
            """
            if (self.l + self.r == 0) or (num <= -self.left[0]):
                heapq.heappush(self.left, -num)
                self.l += 1
            else:
                heapq.heappush(self.right, num)
                self.r += 1
            if self.l - self.r > 1:
                leftMax = heapq.heappop(self.left)
                heapq.heappush(self.right, -leftMax)
                self.l -= 1
                self.r += 1
            elif self.r - self.l > 0:
                rightMin = heapq.heappop(self.right)
                heapq.heappush(self.left, -rightMin)
                self.l += 1
                self.r -= 1

        def findMedian(self):
            """
            Returns the median of current data stream
            :rtype: float
            """
            if self.l == self.r == 0:
                return 0
            elif self.l == self.r:
                return (-self.left[0] + self.right[0]) / 2.0
            else:
                return -self.left[0]