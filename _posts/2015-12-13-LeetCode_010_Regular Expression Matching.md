---
layout: post
title: LeetCode_010_Regular Expression Matching
categories: [LeetCode]
tags: [LeetCode, python, DP]
fullview: true
---
###[Question](https://leetcode.com/problems/regular-expression-matching/)

Implement regular expression matching with support for '.' and '*'.

	'.' Matches any single character.
	'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:

bool isMatch(const char *s, const char *p)

Some examples:

	isMatch("aa","a") → false
	isMatch("aa","aa") → true
	isMatch("aaa","aa") → false
	isMatch("aa", "a*") → true
	isMatch("aa", ".*") → true
	isMatch("ab", ".*") → true
	isMatch("aab", "c*a*b") → true
	
	
### Solution
DP

The key problem is how to deal with the '*' in string p.

There are several cases we need to consider.

Normal cases (without '*'):

1. The same characters:
	* xxx a == xxx a
	* p[i-1] == s[j-1]

2. Current character in p is '.'
	* xxx a == xxx .
	* p[i-1] == '.'
	
Special cases (with '*'):

1. '*' match 0 character in s
	* xxxx == xx a*
	* a[i][j] = a[i-2][j]

2. '*' match 1 character in s
	* xxx a == xx a*
	* a[i][j] = a[i-1][j]
	
3. '*' match 2+ characters in s
	* xxa a == xxa *
	* a[i][j] = a[i-1][j-1] and (p[i-2] == s[j-1])
	
4. '*' match characters with '.' in front
	* xxxx == xx .*
	* a[i][j] = a[i][j-1] and (p[i-2] == '.')

Ps. Think out the solution by thinking from the end. (Start to think the cases from the end of each string to get the state transition equation)

### Code
	class Solution(object):
        def isMatch(self, s, p):
            """
            :type s: str
            :type p: str
            :rtype: bool
            """
            n = len(p)
            m = len(s)
            a = [[False for col in range(m+1)] for row in range(n+1)]
            a[0][0] = True
            for i in xrange(1, n+1):
                cp = p[i-1]
                if (cp == '*') and (i >= 2):
                    a[i][0] = a[i-2][0]
                for j in xrange(1, m+1):
                    if (s[j-1] == cp) or (cp == '.'):
                        a[i][j] = a[i-1][j-1]
                    elif cp == '*':
	                    # match 0  ---- == --a*
                        c1 = a[i-2][j] 
                        # match 1  ---- == ---*
                        c2 = a[i-1][j] 
                        # match 2+  ---? == ---*
                        c3 = a[i-1][j-1] and (s[j-1] == p[i-2])  
                        # ---- == --.*
                        c4 = a[i][j-1] and (p[i-2] == '.') 
                        a[i][j] = c1 or c2 or c3 or c4              
            return a[n][m]


		