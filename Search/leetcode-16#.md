# LeetCode 16. 3Sum Closest  [link](https://leetcode.com/problems/integer-to-roman/)

## Problem description:

> Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>

## Example:

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## Solution:

### Tags:

#### *[Greedy algorithm](https://github.com/yang-233/Algorithm-note/tree/master/Greedy-algorithm)*

### How to do:

> Still using the two pointer approach.

### Code:

```c++
class Solution {
public:

    int threeSumClosest(vector<int> &nums, int target) {
        int ans = INT_MAX, n = nums.size();
        sort(nums.begin(), nums.end());
        for (int i = 0; i < n - 2; ++i) {
            if (i && nums[i] == nums[i - 1])
                continue;
            int l = i + 1, r = n - 1, s;
            while (l < r) {
                if(l > i + 1 && nums[l] == nums[l - 1])
                    ++l;
                if(l >= r)
                    break;
                s = nums[i] + nums[l] + nums[r];
                if (abs(s - target) < abs(ans))
                    ans = s - target;
                if (s == target)
                    return s;
                else {
                    if (s > target)
                        --r;
                    else
                        ++l;
                }
            }
        }
        return ans + target;
    }
};
```

### Time complexity:

#### *O (n^2)*

### Space complexity:

#### *O(1)*

