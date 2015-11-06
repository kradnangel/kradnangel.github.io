---
layout: post
title: LeetCode_069_Sqrt(x)
categories: [LeetCode]
tags: [LeetCode, python, string]
fullview: true
---
###Question
Implement int sqrt(int x).

Compute and return the square root of x.

###Solution
The easiest way to calculate the square root of x is that use 'i' which is increase one by one from 0 to x to check 'i * i' is larger than x or not. When the answer is yes, the square root of x is 'i-1'.

However, this method is too slow. So, we need to think about how to accelerate this method. 

We can increase the i in power of 2. When 'i * i > x', the 'i - 1' is a number which is close to the right number. Then make 'ans = i' and 'i = 1'. Then increase the i in power of 2 again. However, this time, we use '(ans+i)**2 > x' as the criterion. So, we don't assume the 'i' is the square root of x. We assume 'ans + i' is the square root of x. 'i' is the increment.

Every time we make the 'ans' closer to the right number by increasing the i in power of 2. At last, when the 'i == 1' and '(ans + i) ** 2 > x' the 'ans' is the square root of x.

See the details below:

![](/images/069.jpg)

Another solution is dichotomy.


###Code
	class Solution:
		# @param {integer} x
		# @return {integer}
		def mySqrt(self, x):
			ans = 0
			i = 1
			while i != 0:
				i = 1
				while i <= x:
					if (ans + i) ** 2 > x:
						break
					else:
						i = i * 2
				i /= 2
				ans += i

			return ans