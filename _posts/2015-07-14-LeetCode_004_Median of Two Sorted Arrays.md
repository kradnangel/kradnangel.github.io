---
layout: post
title: LeetCode_004_Median of Two Sorted Arrays
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

###Solution
This is a hard question, since we need solve it in O(log (m+n)). So, in every move, the size of question should be reduced by half.

The key idea is to convert this question to the question of finding the 'k'th small number in the two arrays. Here, the k equals to (m+n)/2 if (n+m) is odd. If (n+m) is even, the k should be (m+n)/2 and (m+n)/2 + 1.

How to find the 'k'th small number in two arrays?

We can find the 'k/2'th small number in every array separately. If the length of one array is smaller than 'k/2', we can choose the last one of this array and choose the 'k - length of that array'th of other array.

We will compare the two numbers. if n1['k/2'] > n2['k/2'], it means that n2[0:'k/2'+1] are all smaller than the 'k'th small number. So, we can cut them out. Then try to find the 'k-k/2'th small number in the remaining numbers. Repeat this process till we find the right number -- 'k'th small number.

There are some boundary conditions we will use to stop function and output the right number.

1. When the length of one array is zero, we can find the right number in the other array directly.
2. When the k = 1, we can just output the samller one of n1[0] and n2[0]

Enjor coding!

###Code
	def findMed(n1,n2,k):
        if len(n1) < len(n2):
            return findMed(n2,n1,k)
        if len(n2) == 0:
            return n1[k-1]
        if k == 1:
            return min(n1[0],n2[0])
        k2 = min(k/2, len(n2))
        k1 = k - k2
        
        if n1[k1 - 1] > n2[k2 - 1]:
            return findMed(n1[: k1], n2[k2:], k - k2)
        elif n1[k1 -1] < n2[k2 - 1]:
            return findMed(n1[k1:], n2[:k2], k - k1)
        else:
            return n1[k1 - 1]
    class Solution:
        # @param {integer[]} nums1
        # @param {integer[]} nums2
        # @return {float}
        def findMedianSortedArrays(self, nums1, nums2):
            mn = len(nums1) + len(nums2)
            if mn & 1:
                return findMed(nums1,nums2, mn/2 + 1)
        	else:
                return (findMed(nums1, nums2, mn/2) + findMed(nums1, nums2, mn/2 + 1)) / 2.0
