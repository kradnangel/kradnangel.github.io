---
layout: post
title: Dynamic Programming Summary
categories: [Algorithm]
tags: [Algorithm, DP, 中文]
fullview: true
---
#递推式 Recurrence formula 
阶段 n 的最优解由阶段 n-1 推出。
##Formula
	a[n] = k \* a[n-1] + p \* x[n]
	return a[n]

##Question and Answer
[276. Paint Fence](https://leetcode.com/problems/paint-fence/)

最多连续两个木桩是同色的。这时考虑最后两根木桩颜色的情况。

1. 当最后两根木桩颜色相同

   则最后两根木桩颜色与n-2的木桩颜色不同即可。
   
   则涂色方案数为(k-1) \* a[n-2]
   
2. 当最后两根木桩颜色不同
   
   则不管倒数第二根颜色是什么，倒数第一根和其不同即可。
   
   则涂色方案数为(k-1) \* a[n-1]

	a[n] = (k-1) \* (a[n-1] + a[n-2])


#多状态递推式 Multistate recurrence formula

阶段 n 的最优解仍然由阶段 n-1 推出。但每个阶段将有多个状态。每个状态都由上一个阶段的某几个状态推出。

## Formula (for 3 states)

	a[n][0] = max(a[n][1], a[n][2]) + x[n]
	a[n][1] = max(a[n][0], a[n][2]) + x[n]
	a[n][2] = max(a[n][0], a[n][1]) + x[n]

## Question and Answer
[256. Paint House](https://leetcode.com/problems/paint-house/)

3状态问题。每个房子都有三种涂法。阶段 n 也有三种状态，分别为最后一个房子（房子 n）被涂成红色，被涂成蓝色，被涂成绿色。分别表示涂成对应颜色时，总成本的最小值。

最后一个房子被涂成红色时的最小成本是，涂红成本加上阶段 n-1最后涂蓝／最后吐绿

# 尾部固定式 Rear fixed
阶段 n 的最优解是(阶段 n-1 加当前值) 或者 (仅选择当前值)。

	Value  * * * * * + *
	  
	Case1      = = = + =
	
	Case2              =
 
##Formula
	
	a[n] = max(a[n-1] + x[n], x[n])
	return max(a[n])

##Question and Answer
[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

求最大和子区间。

解法简述：当之前的和加上当前值小于当前值时，抛弃之前所有值选择当前值。否则，加上当前值然后继续。

原理








