---
layout: post
title: LeetCode_068_Text Justification
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

For example, words: 

["This", "is", "an", "example", "of", "text", "justification."]

L: 16.

Return the formatted lines as:

	[
		"This    is    an",
		"example  of text",
		"justification.  "
	]
	
Note: Each word is guaranteed not to exceed L in length.

###Solution
Split the strings list into several groups and abjust every group by adding the blanks.

There are three cases:

1. If this is the last line, just add a blank between words and add extra blanks at the end of string.
2. If there is just one word in this line, add the blanks at the end of string.
3. Otherwise, add extra spaces between words as evenly as possible.

Here, we use 'blknums' to set how many blanks should be added into the every slot and use 'moreblk' to set how many slots should be added one more blank.

Before saving every line, we will delete redundant blanks
which we added into the line.


###Code
	class Solution:
	    # @param {string[]} words
	    # @param {integer} maxWidth
	    # @return {string[]}
	    def fullJustify(self, words, maxWidth):
	        l = len(words)
	        i = 0
	        ans = []
	        while i < l:
	        	nowWidth = len(words[i])
	        	j = i + 1
	        	s = ""
	        	while j < l:
	        		if len(words[j]) + 1 + nowWidth <= maxWidth:
		        		nowWidth += len(words[j]) + 1
		        	else: break
		        	j += 1 
		        
	        	blknums = maxWidth - nowWidth
	        	if j == l:
	        		for h in range(i, j):
		        		s += words[h] + ' '
		        	ans.append(s[:len(s)-1] + ' ' * blknums)
	        	elif j > i + 1:
		        	blknums /= (j - i - 1)
			        moreblk = (maxWidth - nowWidth) - blknums * (j - i - 1)
		        	for h in range(i, j):
		        		s += words[h] + ' ' * (blknums+1) + ' ' * (1 if h - i < moreblk else 0)
		        	ans.append(s[:len(s)-(blknums+1)])
		        else:
		        	ans.append(words[i] + ' ' * blknums)
	        	i = j

	        return ans