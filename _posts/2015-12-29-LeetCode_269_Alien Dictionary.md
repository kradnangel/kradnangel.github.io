---
layout: post
title: LeetCode_269_Alien Dictionary
categories: [LeetCode]
tags: [LeetCode, python, queue, hash]
fullview: true
---
###[Question](https://leetcode.com/problems/alien-dictionary/)
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

For example,
Given the following words in dictionary,

	[
	  "wrt",
	  "wrf",
	  "er",
	  "ett",
	  "rftt"
	]

The correct order is: "wertf".

Note:

1. You may assume all letters are in lowercase.
2. If the order is invalid, return an empty string.
3. There may be multiple valid order of letters, return any one of them is fine.

### Solution
To solve this question, there are two steps:

1. Find the order between letters
2. Find a vaild order for all letters

In step one:

1. record all letters by putting letters of each word in a set.
2. compare two adjacent words, find a order of two letter. Make a new edge and point the letter in word2 from the letter in word1.

In step two:

After step one, we get a directed graph with directed edge representing the order of two nodes/letters. A topological order of this graph is a valid order for all letters. If there is a cycle in this graph, a valid order doesn't exist. 

           
### Code
	from collections import defaultdict
    import operator
    class Solution(object):
        def alienOrder(self, words):
            """
            :type words: List[str]
            :rtype: str
            """
            if words == []: return ''
            n = len(words)
            v = defaultdict(list)
            d = set(words[0])
            flag = True
            for i in xrange(1, n):
                w1 = words[i-1]
                w2 = words[i]
                d = d | set(w2)
                m = min(len(w1),len(w2))
                for j in xrange(m):
                    if w1[j] != w2[j]:
                        break
                if (j < m) and (w1[j] != w2[j]):
                    if w1[j] not in v[w2[j]]:
                        v[w2[j]].append(w1[j]) # w2[j] <- w1[j]
                    if not v.get(w1[j]):
                        v[w1[j]] = []  

            ans = []
            while v:
                # print v
                tmp = []
                for node in v:
                    if len(v[node]) == 0:
                        tmp.append(node)
                if not tmp: 
                    flag = False
                    break
                for node in v:
                    v[node] = list(set(v[node]) - set(tmp))
                for node in tmp:
                    v.pop(node)
                ans += tmp
            
            if flag:
                if len(ans) < len(d):
                    for c in d:
                        if c not in ans:
                            ans.append(c)
                return ''.join(ans)
            else:
                return ''

 