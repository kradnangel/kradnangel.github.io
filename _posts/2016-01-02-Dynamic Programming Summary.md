---
layout: post
title: Dynamic Programming Summary
categories: [Algorithm]
tags: [Algorithm, DP, 中文]
fullview: true
---
## 1. Recurrence formula 
（递推式）

<br>

a[i] 表示阶段i，阶段i 的最优解由阶段 i-1 （及之前的阶段）推出。

### Formula

	a[i] = k \* a[i-1] + p \* v[i]

or

	a[i] = optimal{a[0] ~ a[i-1]}
	
<br>	

### Examples

#### [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

Simple solution O(n^2):

a[i] represent the length of longest increasing subsequence in nums[:i].

	a[i] = max(a[i], a[j] + 1)	# if nums[j] < nums[i]

j is in front of i.

[Better solution](https://discuss.leetcode.com/topic/28738/java-python-binary-search-o-nlogn-time-with-explanation) by using tail array (binary search) O(n log n)


#### [276. Paint Fence](https://leetcode.com/problems/paint-fence/)

最多连续两个木桩是同色的。这时考虑最后两根木桩颜色的情况。

1. 当最后两根木桩颜色相同

   则最后两根木桩颜色与n-2的木桩颜色不同即可。
   
   则涂色方案数为(k-1) \* a[n-2]
   
2. 当最后两根木桩颜色不同
   
   则不管倒数第二根颜色是什么，倒数第一根和其不同即可。
   
   则涂色方案数为(k-1) \* a[n-1]

	a[n] = (k-1) \* (a[n-1] + a[n-2])



#### [139. Word Break](https://leetcode.com/problems/word-break/)

a[i] represent whether the substring of s -- s[:i] can be segmented into a space-separated sequence of dictionary words or not. 

	a[i] = a[j] and (s[j+1:i+1] in wordDict)

a[i] could be True when a[j] is True and s[j+1:i+1] is a dictionary word.


#### [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

a[i] represent the least number of perfect square numbers needed for i.

Go through each square numbers j**2 (smaller than i) for each i (smaller than n).

Find smallest a[i - j**2] for each a[i].


	a[i] = min(a[i-j**2] + 1, a[i])

code: {% gist dccfa256661c8d1939b9530175a60209 %}

<br>

## 1.1. Rear fixed type 

(尾部固定式, 递推变种)

<br>

阶段 n 的最优解是(阶段 n-1 加当前值) 或者 (仅选择当前值)。

	Value  * * * * * + *
	  
	Case1      = = = + =
	
	Case2              =
 
### Formula
	
	a[n] = max(a[n-1] + x[n], x[n])
	
	return max(a[n])

### Examples

#### [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

求最大和子区间。

解法简述：当之前的和加上当前值小于当前值时，抛弃之前所有值选择当前值。否则，加上当前值然后继续。

原理

#### [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)



<br>


## 1.2. Second-order recurrence formula

(二阶递推式)

<br>

a[i,j] represent 
1. the best solution of (0,0) to (i,j) in Matrix
2. or the best solution of 0~i in first string/list and 0~j in second string/list
3. or the best solution of i~j


### Formula

#### Type 1

	# 4 direction, up, down, left, right
	a[i][j] = optimal{a[i-1][j], a[i+1][j], a[i][j-1], a[i][j+1]}
	
#### Type 2
	
	# usually, compare 2 strings or 2 lists
	a[i][j] = optimal{a[i-1][j], a[i][j-1]}
	
#### Type 3

	# need to enumerate the divide-point k
	# so, the time complexity generally is O(n^3)
	a[i][j] = optimal{a[i][k] + a[k][j]}
	
	
### Examples

#### Insert operations

Given a list of integers, you are asked to insert '(', ')', '+', '*' between the integers to get a maximum calculation result.

input1: [1,2,3,4]

return: 36

The best way to insert operations is (1+2)\*3\*4

input1: [-4,3,9]

return 23

The best way to insert operations is -4+3\*9

<br>

Solution is a[i][j] means the maximum caclulation result among input[i:j].

	a[i][j] = max(a[i][j], a[i][k] + a[k+1][j], a[i][k] * a[k+1][j])
	
code: {% gist 8b5712817428f77cd27f0efe3935d288 %}

#### [312. Burst Balloons](https://leetcode.com/problems/burst-balloons/)

a[i][j] represent the maximum coins we can get. (Type 3)

We enumerate the "last time" burst point k between i and j. (Of course, enumerate the step size and start point i as the first two loop)

	a[i][j] = max(a[i][j], a[i][k] + nums[i]*nums[k]*nums[j] + a[k][j])
	
code: {% gist f1bd27ed6bda63a27b739f9415fbdd70 %}


<br>

---

## 2. Multistate recurrence formula

（多状态递推式）

<br>

阶段 n 的最优解仍然由阶段 n-1 推出。但每个阶段将有多个状态。每个状态都由上一个阶段的某几个状态推出。

### Formula (for 3 states)

	a[n][0] = max(a[n][1], a[n][2]) + x[n]
	a[n][1] = max(a[n][0], a[n][2]) + x[n]
	a[n][2] = max(a[n][0], a[n][1]) + x[n]

### Examples

#### [256. Paint House](https://leetcode.com/problems/paint-house/)

3状态问题。每个房子都有三种涂法。阶段 n 也有三种状态，分别为最后一个房子（房子 n）被涂成红色，被涂成蓝色，被涂成绿色。分别表示涂成对应颜色时，总成本的最小值。

最后一个房子被涂成红色时的最小成本是，涂红成本加上阶段 n-1最后涂蓝／最后吐绿

#### [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

Need 3 States for this task -- buy/bought (s1), sell (s2) and cooldown/none (s3).

The start state is at cooldown/none. Then, we can choose buy stock or do nothing. 
	
1. If we buy, we move to buy/bought state and pay for stock. 
2. If we do nothing, we stay at cooldown/none.

When we at buy/bought state, we have bought stock, so we can hold the stock to wait or sell it at this moment. 

1. If we hold, we stay at buy/bought state. 
2. If we sell, we move to sell state and get money.

When we at sell state, we can only move to cooldown/none state.

The end state is sell or cooldown/none state (It's no benefit to buy at last moment.)

![](/images/dp0.jpg)

So, the formulas are:
		
		# record old state
        t2 = s2
        t1 = s1
        t0 = s0
        
        # renew each state
        s0 = max(t0, t2)
        s1 = max(t1, t0 - prices[i])
        s2 = t1 + prices[i]

code: {% gist dd323796ea3d7f83b7bf1907620392f6 %}


<br>

---

### 3. Memorization search

 (记忆化搜索)

<br>

#### [403. Frog Jump](https://leetcode.com/problems/frog-jump/)

DFS + Memorization, save the result of the state we have visited.

For this question, if the frog uses step size 'k' to jump to current stone "s", but it can not reach the last stone. We will add (k, s) to 'not work' set. So, if next time, we revisit this stone by this step size, we will return 'False' directly instead of keeping trying.

code: {% gist ce51ff0e216edf0da0e7d57b254ff0da %}

<br>

---

### 4. Others

#### [354. Russian Doll Envelopes](https://leetcode.com/problems/russian-doll-envelopes/)

Binary Search + DP



<br>

---

## Summary

大部分的DP题目，只要返回一个值就好了。这样，用一个数组去记录每一个状态的最优值就好了。

但有些DP需要最优解的所有组成情况，这时候可能就需要用递归(recursive)来帮助纪录所有组成情况了。

思考以下题目：

[140. Word Break II](https://leetcode.com/problems/create-maximum-number/)

<br>

DP是个很好的idea，但是遍历所有情况的时候是很耗时间的（使用for-loop），特别是如果遍历过程中会遇到很多无用解时。这时候，采取递归的记忆化搜索会快一些，当遇到无用解时，提前退出这次枚举（剪枝）。或者换一个思路思考这个问题（也可能仍是DP）。

思考以下题目：

[321. Create Maximum Number](https://leetcode.com/problems/create-maximum-number/)

