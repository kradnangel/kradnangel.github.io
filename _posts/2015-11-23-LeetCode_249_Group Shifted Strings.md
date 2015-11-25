---
layout: post
title: LeetCode_249_Palindrome Permutation
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a string, we can “shift” each of its letter to its successive letter, for example: “abc” -> “bcd”. We can keep “shifting” which forms the sequence:

	"abc" -> "bcd" -> ... -> "xyz"

Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.
For example,

given: 

["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"], 

Return:

	[
      ["abc","bcd","xyz"],
      ["az","ba"],
      ["acef"],
      ["a","z"]
    ]

    
###Solution
The key idea is that if two strings are the same shifting sequence, the distance between every two corresponding chars should be the same. 

So, just process the string one by one and add them to answer list. Besides, we do not need to compare one string to every strings in answer list. Just compare that one with every first string of inner in the answer list. 


###Code
	class Solution(object):
        def groupStrings(self, strings):
            """
            :type strings: List[str]
            :rtype: List[List[str]]
            """
            def isSame(s,t):
                flag = True
                k = ((26 + ord(s[0])) - ord(t[0])) % 26
                for i in range(1,len(s)):
                    if ((26 + ord(s[i])) - ord(t[i])) % 26 != k:
                        flag = False
                return flag 
            if not strings:
                return []
            ans = [[strings.pop()]]
            for s in strings:
                flag = True
                for i in range(len(ans)):
                    if (len(s) == len(ans[i][0])) and isSame(s,ans[i][0]):
                        ans[i].append(s)
                        flag = False
                        break
                if flag:
                    ans.append([s])
            for i in range(len(ans)):
                ans[i].sort()
            return sorted(ans)