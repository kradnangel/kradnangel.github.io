---
layout: post
title: LeetCode_316_Remove Duplicate Letters
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###[Question](https://leetcode.com/problems/remove-duplicate-letters/)
Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

Example:

Given "bcabc"

Return "abc"

</br>

Given "cbacdcbc"

Return "acdb"
    
###[Solution](https://leetcode.com/discuss/73777/easy-to-understand-iterative-java-solution)


###Code
	class Solution(object):
        def removeDuplicateLetters(self, s):
            """
            :type s: str
            :rtype: str
            """
            t = {}; i = 0
            for c in s:
                t[c] = i
                i += 1
            o = sorted(zip(t.values(),t.keys()))
            print o
            start,ans = 0,[]
            for item in o:
                p, a = item[0], item[1]
                if t[a] > -1:
                    j = -1; c = ''
                    while (j != p) and (c != a):
                        j = p
                        for i in range(start, p):
                            if (t[s[i]] > -1) and ((s[i]<s[j]) or (s[i]==s[j]) and (i < j)):
                                j = i
                        c = s[j]
                        t[c] = -1
                        ans.append(c)
                        start = j+1
            
            return ''.join(ans)