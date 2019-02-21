# LeetCode 560. Subarray Sum Equals K [link](https://leetcode.com/problems/subarray-sum-equals-k/)

## Problem description:

> Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.
>
> **Note:**
>
> 1. The length of the array is in range [1, 20,000].
> 2. The range of numbers in the array is [-1000, 1000] and the range of the integer **k** is [-1e7, 1e7].

## Example:

>```
>Input:nums = [1,1,1], k = 2
>Output: 2
>```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

### How to do:

> Use hash map to record the number of the prefix sums of the array. If the *sum* is same as the nums, *sum[r] - sum[l]* is the sum in range of (i,j]. if the *sum's length = nums's length + 1(sum[0] = 0)*, *sum[r] - sum[l]* is the sum in range of [i,j). And, initial {0, 1} is for solve the case that sum = k (ex: if array is [0, 0] , k = 0, the answer is 3 ).
>
> Inspired by [this blog](http://www.cnblogs.com/grandyang/p/6810361.html).

### Code:

```c++
class Solution {
public:
    int subarraySum(vector<int>& a, int k) {
        int res = 0, sum = 0;
        unordered_map<int, int> m{{0, 1}};//value -> the number of occurrences
        for(auto i : a) {
            sum += i;
            if(m.find(sum - k) != m.end())
                res += m[sum - k];
            if(m.find(sum) == m.end())
                m[sum] = 1;
            else
                ++m[sum];
        }
        return res;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

