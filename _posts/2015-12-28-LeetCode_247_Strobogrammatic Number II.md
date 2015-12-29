---
layout: post
title: LeetCode_247_Strobogrammatic Number II
categories: [LeetCode]
tags: [LeetCode, python, iteration]
fullview: true
---
###[Question](https://leetcode.com/problems/strobogrammatic-number-ii/)

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

For example,

Given n = 2, return ["11","69","88","96"].
       
### Solution
What we need to do is just iteratively generate the answers layer by layer. If the n is odd, we start at ['0','1','8']. Otherwise, we start at ['']. Just like palindromic numbers. Then add the two corresponding numbers at the left and right separately.

We should notice that at the outermost layer, we couldn't use '0'.     
           
### Code
	class Solution(object):
        def findStrobogrammatic(self, n):
            """
            :type n: int
            :rtype: List[str]
            """
            ans = ['0','1','8'] if n % 2 else ['']
            while n > 1:
                n -= 2
                ans = [l + m + r for l,r in ['00','11','69','96','88'][n<2:] for m in ans]
            return ans
            
### [Reference](https://leetcode.com/discuss/50405/3-lines-ruby-5-lines-python)
            
                    