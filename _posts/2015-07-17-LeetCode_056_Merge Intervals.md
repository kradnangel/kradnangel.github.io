---
layout: post
title: LeetCode_056_Merge Intervals
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given a collection of intervals, merge all overlapping intervals.

For example,

Given [1,3],[2,6],[8,10],[15,18],

return [1,6],[8,10],[15,18].

###Solution
Here, first, we just use the qsort to sort the intervals by the 'start'.

Second, from the beginning, compare the 'end' of the first interval with the 'start' of the second interval.

If 0.end >= 1.start, they have overlapping. So, merge them.
If 0.end < 1.start. They don't have overlapping. So, add the first interval to the answer list.

At last, return the answer list.

###Code
	def qsort(L):
		if len(L) <= 1: return L
		return qsort([lt for lt in L[1:] if lt.start < L[0].start]) + [L[0]] + qsort([ge for ge in L[1:] if ge.start >= L[0].start])

	class Solution:
		# @param {Interval[]} intervals
		# @return {Interval[]}
		def merge(self, intervals):
			if (intervals == []):
				return intervals
			ans = []	
			a = qsort(intervals)
			while len(a) > 1:
				if a[0].end >= a[1].start:
					a[0].end = max(a[0].end, a[1].end)
					a.pop(1)
				else:
					ans.append(a[0])
					a.pop(0)
			ans.append(a[0])
			return ans