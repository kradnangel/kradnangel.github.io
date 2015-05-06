---
layout: post
title: Divide two integers
categories: [LeetCode]
tags: [LeetCode, python]
fullview: true
---
###Question
Divide two integers without using multiplication, division and mod operator.

###Solution
Firstly, we can find the easiest way to solve it: Dividend keeps subtracting divisor until Dividend becomes 0.

However, this method is too slow.

The improved method is that dividend subtract the power of divisor.

Dividend = divisor * 2^a + divisor * 2^b + ....

For example:

47/7 = 7 * 2^2 + 7 * 2^1 + 5

The answer is 2^2 + 2^1 = 6

###Code
	class Solution:  
        # @return an integer  
        def divide(self, dividend, divisor):  
            if divisor == 1:  
                return dividend  
            if divisor == -1:  
                return -dividend  
              
            flag = True  
            if divisor < 0:  
                divisor = -divisor  
                flag = not flag  
            if dividend < 0:  
                dividend = -dividend  
                flag = not flag  
                  
            if divisor > dividend:  
                return 0  
                  
            ans = 0  
            i = 1  
            k = divisor  
            while k+k < dividend :  
                k = k << 1  
                i = i << 1  
            dividend -= k  
            ans += i  
            while dividend > 0:  
                while k > dividend:  
                    k = k >> 1  
                    i = i >> 1  
                dividend -= k  
                ans += i  
            if not flag:  
                ans = -ans  
            return ans