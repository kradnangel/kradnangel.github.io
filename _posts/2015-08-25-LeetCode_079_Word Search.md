---
layout: post
title: LeetCode_079_Word Search
categories: [LeetCode]
tags: [LeetCode, python, matrix]
fullview: true
---
###Question
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given board =

	[
		"ABCE",
		"SFCS",
		"ADEE"
	]
	
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.

###Solution
At first, find all start points. It means that find all the positions of the first char of the word in the matrix. 

Then, from every start points, we search next chars in the matrix in four direction (left, right, up, down) till we find all chars or we cannot find all chars.

Here, we use a matrix 'f' to mark which char in matrix is unused. Use a list 'p' to record the search path.

The 'x', 'y' here represent the current position.


###Code
	class Solution(object):
		def exist(self, board, word):
			n = len(board)
			m = len(board[0])	
			f = [[True for col in range(m)] for row in range(n)]
			d = [[0,1],[1,0],[-1,0],[0,-1]]
			p = []
			end = len(word)
			startList = []
			for i in range(n):
				for j in range(m):
					if board[i][j] == word[0]:
						startList.append([i,j])
			if startList == []:
				return False
			for startP in startList:
				i = 1
				p.append(-1)
				x = startP[0]
				y = startP[1]
				f[x][y] = False
				while i in range(1, end):
					for j in range(p[-1] + 1, 4+1):
						if (j < 4) and (x+d[j][0] in range(n)) and (y+d[j][1] in range(m)):
							if f[x+d[j][0]][y+d[j][1]] and (board[x+d[j][0]][y+d[j][1]] == word[i]):
								break
					if j == 4:
						i -= 1
						p.pop()
						f[x][y] = True
						if p:
							back = p[-1]
						else:
							break
						x -= d[back][0]
						y -= d[back][1]
					else:
						i += 1
						p[-1] = j
						p.append(-1)
						x += d[j][0]
						y += d[j][1]
						f[x][y] = False

				if i == end:
					return True

			return False