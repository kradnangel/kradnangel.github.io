---
layout: post
title: LeetCode_289_Game of Life
categories: [LeetCode]
tags: [LeetCode, python, matrix]
fullview: true
---
###Question
According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

Any live cell with fewer than two live neighbors dies, as if caused by under-population.
Any live cell with two or three live neighbors lives on to the next generation.
Any live cell with more than three live neighbors dies, as if by over-population..
Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
Write a function to compute the next state (after one update) of the board given its current state.

Follow up: 
Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?
    
###Solution
This question is not hard. The key point is processing every case well. 

First of all, In order to solve it in-place, we need a new coding scheme. I use binary coding. 2^1 shows the old state and 2^0 shows the current state.

There are several cases needed to be considered first. 

1. No cell, pass.
2. only 1 cell in matrix, just return [[0]] because of too few cells.
3. only one row or one column. The first and last cells must be 0. In the middle, cell would be live(1) if left and right is 1, otherwise dead(0).

For normal case (n>=2 and m>=2), deal with corners first, then deal with first/last row and first/last column. Deal with the inside cell at last. 

###Code
	class Solution(object):
        def gameOfLife(self, board):
            """
            :type board: List[List[int]]
            :rtype: void Do not return anything, modify board in-place instead.
            """
            def state(s, k):    
                new = s<<1
                if (s == 0) and (k == 3):
                    new += 1
                elif (s == 1) and ((k == 2) or (k == 3)):
                    new += 1
                return new        
            if (board == [[]]):
                pass
            elif (board == [[0]]) or (board == [[1]]):
                board[0][0] = 0
            else:
                m = len(board)
                n = len(board[0])
                if m == 1:
                    board[0][0] <<= 1
                    for j in xrange(1, n-1):
                        now = board[0][j]
                        board[0][j] = state( now, (board[0][j-1]>>1) +(board[0][j+1]) )
                    board[0][n-1] <<= 1
                elif n == 1:    
                    board[0][0] <<= 1
                    for i in xrange(1, m-1):
                        now = board[i][0]
                        board[i][0] = state(now, (board[i-1][0]>>1)+(board[i+1][0]))
                    board[m-1][0] <<= 1
                else:
                    # binary coding. 2^1 as old state, 2^0 as new state 
                    for i in xrange(m):
                        for j in xrange(n):
                            now = board[i][j]
                            if (i,j) == (0,0):
                                board[i][j] = state(now, sum([board[1][0],board[0][1],board[1][1]]))
                            elif (i,j) == (0, n-1):
                                board[i][j] = state(now, sum([board[0][n-2]>>1,board[1][n-1],board[1][n-2]]))
                            elif (i,j) == (m-1,0):
                                board[i][j] = state(now, sum([board[m-2][0]>>1,board[m-1][1],board[m-2][1]>>1]))
                            elif (i,j) == (m-1,n-1):
                                board[i][j] = state(now, sum([board[m-1][n-2]>>1,board[m-2][n-1]>>1,board[m-2][n-2]>>1]))
                            elif i == 0:
                                board[i][j] = state(now, sum([board[i][j-1]>>1, board[i][j+1], board[i+1][j-1],board[i+1][j],board[i+1][j+1]]))
                            elif i == m-1:
                                board[i][j] = state(now, sum([board[i][j-1]>>1, board[i][j+1], board[i-1][j-1]>>1, board[i-1][j]>>1, board[i-1][j+1]>>1]))
                            elif j == 0:
                                board[i][j] = state(now, sum([board[i-1][j]>>1, board[i+1][j], board[i-1][j+1]>>1, board[i][j+1], board[i+1][j+1]]))
                            elif j == n-1:
                                board[i][j] = state(now, sum([board[i-1][j]>>1, board[i+1][j], board[i-1][j-1]>>1, board[i][j-1]>>1, board[i+1][j-1]]))
                            else:
                                board[i][j] = state(now, sum([board[i-1][j-1]>>1, board[i-1][j]>>1, board[i-1][j+1]>>1, board[i][j-1]>>1,
                                                             board[i][j+1], board[i+1][j-1], board[i+1][j], board[i+1][j+1]]))
                    print board                            
                for i in xrange(m):
                    for j in xrange(n):
                        board[i][j] %= 2