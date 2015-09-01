---
layout: post
title: LeetCode_093_Restore IP Addresses
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:
Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

	
###Solution
The idea is that find all possible division and test them by regular expression.


###Code
	import re

	class Solution(object):
	    def restoreIpAddresses(self, s):
	        """
	        :type s: str
	        :rtype: List[str]
	        """
	        ans = []
	        n = len(s)
	        if (n < 4) or (n > 12):
	        	return ans

	        p = re.compile(r'\b(?:(?:25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[0-9])\.){3}(?:25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[0-9])\b', re.IGNORECASE)
	        d = [1,2,3]
	        while d[2] < n:
	        	ip = s[0:d[0]] + '.' + s[d[0]:d[1]] + '.' + s[d[1]:d[2]] + '.' + s[d[2]:]
	        	print ip
	        	if re.findall(p, ip) and (ip not in ans):
	        		ans.append(ip)
	        	i = 2
	        	d[i] += 1
	        	while (i > 0) and (d[i] > n - 3 + i):
	        		i -= 1
	        		d[i] += 1
	        	if i < 0:
	        		break
	        	while i < 2:
	        		i += 1
	        		d[i] = d[i-1] + 1

	        return	ans