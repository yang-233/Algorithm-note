# LeetCode 18. 4Sum [link](https://leetcode.com/problems/4sum/)

## Problem description:

> Given an array `nums` of *n* integers and an integer `target`, are there elements *a*, *b*, *c*, and *d* in `nums` such that *a* + *b* + *c* + *d* = `target`? Find all unique quadruplets in the array which gives the sum of `target`.
>
> **Note:**
>
> The solution set must not contain duplicate quadruplets.

## Example:

```
Given array nums = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)*

### How to do:

> The approach as same as the *3Sum*.

### Code:

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int> &nums, int target) {
        vector<vector<int>> ans;
        int n = nums.size();
        sort(nums.begin(), nums.end());
        for (int i = 0; i < n - 3; ++i) {
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            for (int j = i + 1; j < n - 2; ++j) {
                if (j > i + 1 && nums[j] == nums[j - 1])
                    continue;
                int l = j + 1, r = n - 1, s;
                while (l < r) {
                    while (l > j + 1 && nums[l] == nums[l - 1])
                        ++l;
                    if (l >= r)
                        break;
                    s = nums[i] + nums[j] + nums[l] + nums[r];
                    if (s == target) {
                        vector<int> tmp;
                        tmp.push_back(nums[i]);
                        tmp.push_back(nums[j]);
                        tmp.push_back(nums[l]);
                        tmp.push_back(nums[r]);
                        ans.push_back(tmp);
                        ++l;
                        --r;
                    } else {
                        if (s > target)
                            --r;
                        else
                            ++l;
                    }
                }
            }
        }
        return ans;
    }
};
```

### Time complexity:

#### *O (n^3)*

### Space complexity:

#### *O(1)*

