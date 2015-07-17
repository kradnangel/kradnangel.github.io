---
layout: post
title: LeetCode_057_Insert Interval
categories: [LeetCode]
tags: [LeetCode, python, list]
fullview: true
---
###Question
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:

Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

Example 2:

Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

###Solution
There are several cases that we have to deal with:

![](/images/057.jpg)

Just code.

###Code
	class Solution:
		# @param {Interval[]} intervals
		# @param {Interval} newInterval
		# @return {Interval[]}
		def insert(self, intervals, newInterval):
			if intervals == []:
				return [newInterval]
			ans = []
			while len(intervals) > 0:
				if intervals[0].end < newInterval.start:
					ans.append(intervals[0])
					intervals.pop(0)
				else:
					break
			while len(intervals) > 0:
				x = intervals[0]
				if (x.end >= newInterval.start) & (x.end <= newInterval.end):
					newInterval.start = min(newInterval.start, x.start)
				elif (x.start <= newInterval.end) & (x.end >= newInterval.end):
					newInterval.end = max(newInterval.end, x.end)
					newInterval.start = min(newInterval.start, x.start)
				elif x.start > newInterval.end:
					break
				intervals.pop(0)

			ans.append(newInterval)
			ans = ans + intervals	

			return ans