---
layout: post
title: LeetCode_081_Search in Rotated Sorted Array II
categories: [LeetCode]
tags: [LeetCode, python, sort]
fullview: true
---
###Question
Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.

###Solution
Let's see a case:

	[1,1,1,1,3,1,1]
	
We will find that nums[mid] == nums[left] and nums[mid] == nums[right]. We cannot determine which part the target may be in. 

Thereform, we need add one more case in our program based on the program which is used in "033 Search in Rotated Sorted Array". When nums[mid] == nums[left] and nums[mid] == nums[right], we just move "left" one step forword (left += 1).

Also, in this case, the worst-case for run-time complexity is O(n).


###Code
	class Solution(object):
        def search(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            left = 0
            right = len(nums) - 1
            ans = False

            while left <= right:    
                mid = (left + right) / 2
                if target == nums[mid]:
                    ans = True
                    break
                # This is the new part    
                elif (nums[mid] == nums[left]) and (nums[mid] == nums[right]):
                    left = left + 1
                # --------------------
                elif target < nums[mid]:
                    if (target < nums[left]) and (nums[left] <= nums[mid]):
                        left = mid + 1
                    else:
                        right = mid - 1
                elif target > nums[mid]:
                    if (target > nums[right]) and (nums[mid] <= nums[right]):
                        right = mid - 1
                    else:
                        left = mid + 1

            return ans