---
layout: post
title: LeetCode_161_One Edit Distance
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given two strings S and T, determine if they are both one edit distance apart.
    
###Solution
There are three cases of one edit distance.
1. change one char
2. add one char
3. delete one char

2 and 3 can be seen as one kind of edit.

Therefore,

1. When the lengths of s and t are the same, calculate how many chars are different in two strings.
2. When the difference of lengths of s and t is 1, take the longer one as s1, the other one as s2. 
	1. From head, find the first different char. (If doesn't exist, return False)
	2. delete it from s1
	3. calculate the difference of two strings
	4. if difference == 0, then return True. Otherwish, return False.
	

###Code
	class Solution(object):
        def isOneEditDistance(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: bool
            """
            def distance(s,t):
                return sum(map(lambda c1,c2: c1 != c2, s,t))
            n = len(s)
            m = len(t)
            flag = False
            if n == m:
                if distance(s,t) == 1:
                    flag = True
            elif abs(n-m) == 1:
                s1 = s if n >= m else t
                s2 = t if n >= m else s
                n = len(s1);    m = len(s2);
                i = 0
                while i < m:
                    if s1[i] != s2[i]:
                        break
                    i += 1
                if i < m:
                    if distance(s1[:i] + s1[i+1:], s2) == 0:
                        flag = True
                else:
                    flag = True

            return flag