# [LeetCode 128. Longest Consecutive Sequence](<https://leetcode.com/problems/longest-consecutive-sequence/>) 

## Problem description:

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(*n*) complexity.

## Example:

>```
>Input: [100, 4, 200, 1, 3, 2]
>Output: 4
>Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
>```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

#### How to do:

> Use an hash table to record  every number. For *i* in list, we remove it and find *i -1* , *i+1* and remove then then until they not in the hash table. 

### Code:

```python
class Solution:
    def longestConsecutive(self, nums) -> int:
        if len(nums) == 0:
            return 0
        s = set(nums)
        maxn = 1
        for i in nums:
            if i in s:
                l, r = i - 1, i + 1
                s.remove(i)
                while l in s:
                    s.remove(l)
                    l -= 1;
                while r in s:
                    s.remove(r)
                    r += 1
                maxn = max(maxn, r - l - 1)
        return maxn
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

