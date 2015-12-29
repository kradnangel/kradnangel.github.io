---
layout: post
title: LeetCode_146_LRU Cache
categories: [LeetCode]
tags: [LeetCode, python, queue, hash]
fullview: true
---
###[Question](https://leetcode.com/problems/lru-cache/)
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.

set(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.
  
### Solution

#### 1. Hash tables & List
The first idea is that use a hash table (dict in python) to recode the <key, value> and use a list to record the order of the keys. 

For 'get', O(1) is used to check whether the key is in the hash table or not and return the value. But, O(n) may be used to delete the key in the list when the key exists. So, the total time-complexity of 'get' is O(n). 

The time-complexity of 'set' also is O(n) because the renewing the key also need to delete the key in the list and then add the key back.

#### 2. Add Lazy deletion
In order to reduce the time-complexity, lazy deletion could be used in manage keys in the list. What we need extra is a hash table which is used to record the times a key has been updated. So, when we need to renew the position of a key ('get' or 'set'), we can just add the key to the right of list and mark it as updated in the 'hasUpdated' hash table. When we add a new number to the cache, we need to pop out the leftmost key in the list. So, at this time, when we pop out a key, we need to check this key has been updated or not. If not, just pop it out and add new key into the rightmost of list. If yes, pop it out and update the 'hasUpdated' hash table. Then pop out a key again and check it until a key hasn't been updated before. Then pop it out and add new key.

After improvement, the time-complexity of 'get' is O(1) since we just search the value of key and do lazy deletion.

The time-complexity of 'set' is still O(n) because the operation 'pop from leftmost' for list is O(n).

#### 3. Replace list as queue
Because the operation in the list which is used to record the order of key are only 'push into the rightmost' and 'pop from the leftmost', we can replace the list(array) as queue which is implemented by linked-list. This change could reduce the time-complexity of 'set' from O(n) to O(1).
           
### Code
	from collections import deque
    class LRUCache(object):

        def __init__(self, capacity):
            """
            :type capacity: int
            """
            self.d = {}
            self.n = capacity
            self.stack = deque([])
            self.hasUpdated = {}

        def get(self, key):
            """
            :rtype: int
            """
            k = self.d.get(key, '-1')
            if k != -1:
                self.hasUpdated[key] = self.hasUpdated.get(key,0) + 1
                self.stack.append(key)
            return int(k)

        def set(self, key, value):
            """
            :type key: int
            :type value: int
            :rtype: nothing
            """
            if self.d.get(key, -1) != -1:
                self.d[key] = value
                self.hasUpdated[key] = self.hasUpdated.get(key,0) + 1
                self.stack.append(key)
            else:
                if self.n > 0:
                    self.n -= 1
                else:
                    oldKey = self.stack.popleft()
                    while self.hasUpdated.get(oldKey,0) > 0:
                        self.hasUpdated[oldKey] -= 1
                        oldKey = self.stack.popleft()
                    self.d.pop(oldKey)
                self.d[key] = value
                self.stack.append(key)

 