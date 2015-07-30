---
layout: post
title: LeetCode_071_Simplify Path
categories: [LeetCode]
tags: [LeetCode, python, numbers]
fullview: true
---
###Question
Given an absolute path for a file (Unix-style), simplify it.

For example,

path = "/home/", => "/home"

path = "/a/./b/../../c/", => "/c"

Corner Cases:

Did you consider the case where path = "/../"?

In this case, you should return "/".

Another corner case is the path might contain multiple 
slashes '/' together, such as "/home//foo/".

In this case, you should ignore redundant slashes and 
return "/home/foo".

###Solution
This question and my code both are a bit complicated.

You should consider several cases.

In general case, what we need to do is that pick up the first folder name, add it to the stack (here, I use a list) and delete it from the path. 

Here I use '/[^/^\s]*/' to pick up the folder name from the path. The pattern likes this: '/home/'.

In other cases, If we meet '/../', we pop the first folder name from stack (if it's not empty). If we meet '//' or '/./', we do nothing.

Final, before output, we need to consider this case '/home/foo'. I mean, the '/foo' just have a left '/'. So, I need to use a different pattern '/[^/^\s]*' to pick it out and deal with it.

Ps. We also need to consider that, after processing, if the stack is empty, we need to output '/' instead of ''.


###Code
	class Solution:
		# @param {string} path
		# @return {string}
		def simplifyPath(self, path):
			path = path.strip()
			i = 0
			l = len(path)
			a = []
			p = re.compile(r'/[^/^\s]*/')
			p2 = re.compile(r'/[^/^\s]*')
			while p.match(path):
				f = p.match(path)
				fg = f.group()
				fgl = len(fg)
				if (fg == '/../'):
					if a:
						a.pop()
				elif (fg == '//') or (fg == '/./'):
					pass
				else:	
					a.append(fg[:fgl-1])
				path = path[fgl-1:]

			if p2.match(path):
				f = p2.match(path)
				fg = f.group()
				fgl = len(fg)
				if (fg == '/..'):
					if a:
						a.pop()
				elif (fg == '/') or (fg == '/.'):
					pass
				else:	
					a.append(fg)
					path = ''

			ans = ''
			for x in a:
				ans += x
			if ans == '':
				ans = '/'
			print path
			return ans