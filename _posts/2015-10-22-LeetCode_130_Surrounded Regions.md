---
layout: post
title: LeetCode_130_Surrounded Regions
categories: [LeetCode]
tags: [LeetCode, python, matrix, traversal]
fullview: true
---
###Question
Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,

	X X X X
	X O O X
	X X O X
	X O X X

After running your function, the board should be:

	X X X X
	X X X X
	X X X X
	X O X X

###Solution
The key point of this question is changing your mind. 

At the beginning, I was thinking to check every 'O' is in surrounded region or not. So, I checked every 'O'.

1. If it is in board, it's a bad 'O'. Mark it as 'B'.
2. If some direction are 'B', it's also a bad '0'. Mark it as 'B'.
3. If some direction are 'O', the state of this 'O' depends on the state of these 'O'. So, check these 'O'.
4. If all around it are 'X', it's in surrounded region. Mark it as 'X'.

This solution leads to system stack overflow.

We do not need to check every 'O' one by one. What we should do is just doing search based on the 'O' which is in the border. So, they are bad 'O's and what we do is finding the 'O' is in the same region with these bad 'O' and marking it as bad 'O'.

Then, at last, change every 'O' to 'X' and change every 'B' to 'O'.

###Code
	class Solution(object):
        def solve(self, board):
            """
            :type board: List[List[str]]
            :rtype: void Do not return anything, modify board in-place instead.
            """
            n = len(board)
            if n > 0:
                m = len(board[0])
            else: m = 0
            visited = [[True for j in range(m)] for i in range(n)]
            d = [[0,1],[1,0],[-1,0],[0,-1]]
            b = map(lambda x:list(x), board)
            for i in range(n):
                for j in range(m):
                    if board[i][j] == 'O':
                        visited[i][j] = False
            for i in range(n):
                if b[i][0] == 'O':
                    b[i][0] = 'B'
                if b[i][m-1] == 'O':
                    b[i][m-1] = 'B'                
            for j in range(m):
                if b[0][j] == 'O':
                    b[0][j] = 'B' 
                if b[n-1][j] == 'O':
                    b[n-1][j] = 'B'                 
            
            def markB(x,y):
                stack = [(x,y)]
                while stack:
                    # i = stack[0][0]; j = stack[0][1]
                    (i,j) = stack.pop()
                    visited[i][j] = True
                    for h in range(4):
                        if not((i+d[h][0] > n-1) or (i+d[h][0] < 0) or (j+d[h][1] > m-1) or (j+d[h][0] < 0)):
                            if b[i+d[h][0]][j+d[h][1]] == 'O':
                                b[i+d[h][0]][j+d[h][1]] = 'B'
                                stack.append((i+d[h][0],j+d[h][1]))


            for i in range(n):
                for j in range(m):
                    if (b[i][j] == 'B') and (not visited[i][j]):
                        markB(i,j)

            for i in range(n):
                for j in range(m):
                    if b[i][j] == 'O':
                        b[i][j] = 'X'                              
            for i in range(n):
                for j in range(m):
                    if b[i][j] == 'B':
                        b[i][j] = 'O' 

            for i in range(n):
                board[i] = ''.join(b[i])