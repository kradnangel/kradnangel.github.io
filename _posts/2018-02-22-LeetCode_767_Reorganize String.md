---
layout: post
title: LeetCode_767_Reorganize String
categories: [LeetCode]
tags: [LeetCode, python, String]
fullview: true
---
### [Question](https://leetcode.com/problems/flood-fill/description/)
Given a string S, check if the letters can be rearranged so that two characters that are adjacent to each other are not the same.

If possible, output any possible result.  If not possible, return the empty string.

Example 1:

Input: S = "aab"
Output: "aba"
Example 2:

Input: S = "aaab"
Output: ""
Note:

S will consist of lowercase letters and have length in range [1, 500].

### Solution
String process. 

In order to meet the requirement, we need to find the most common character X in the string S (let's say it occurs K times) and check whether the remain characters can fill the blank between X. 

e.g. here K = 5

X_X_X_X_X

At least there should be K-1 other characters to fill the blank between X.

So, first of all, we count the number of each charactors and find the most common character X and check whether we can make it. 

If it's possible. We can generate the reorganized string by:

We start at a empty string. Then, each time, we find the most common characters in the remain characters (it should be same as the last character we just put into the result string)and put it into the result string. keep doing until we used all characters.

e.g. aaaabbc

a:4, b:2, c:1

1st: a is the most common character, put a into the result string, result string:"a"

2nd: a is still the most common character, but the last character is 'a', so we use 'b'. result string: "ab"

3rd: a is still the most common character, we got "aba"

....

we may get: "ababaca"


### Code
{% gist 6af149ac98df3341ea0c35a1d64a462c %}          

