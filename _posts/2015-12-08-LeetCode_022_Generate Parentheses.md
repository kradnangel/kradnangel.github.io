---
layout: post
title: LeetCode_022_Generate Parentheses
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

"((()))", "(()())", "(())()", "()(())", "()()()"
    
###Solution
DFS.

Left, add '(', if number of '(' is less than n.

Right, add ')', if number of ')' is less than '('.


###Code
	class Solution(object):
        def generateParenthesis(self, n):
            """
            :type n: int
            :rtype: List[str]
            """
            def addP(l,r,s):
                ans = []
                if (l == r == 0):
                    ans.append(s)
                if (l > 0):
                    ans += addP(l-1,r,s+'(')
                if (r > 0) and (l < r):
                    ans += addP(l,r-1,s+')')
                return ans
            return addP(n,n,'')
