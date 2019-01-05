# LeetCode 1. Two Sum [link](https://leetcode.com/problems/two-sum/)

## Problem description:

> Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
>
> You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

## Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solution:

### How to do:

> We want to find a pair of  *i*  and  *j* satfity this condition:
> $$
> nums[i] + nums[j] = target
> $$
>
> First, record every values' index and sort the array. Then, for each *i*, use binary search find the 
>
> *target - nums[i]* from *nums[i+1]* to *nums[n-1]*.

### Code:

```c++
class Solution {
public:

    int binary_search(vector<pair<int,int>> &temp, int l, int r, int value) {
        while (l <= r) {
            int mid = (l + r) / 2;
            if (temp[mid].first == value)
                return mid;
            else {
                if (temp[mid].first < value)
                    l = mid + 1;
                else
                    r = mid - 1;
            }
        }
        return -1;
    }
    
    vector<int> twoSum(vector<int> &nums, int target) {
        vector<int> ans;
        vector<pair<int,int>> temp;
        int n = nums.size();
        for (int i = 0; i < n; ++i)//record the index
            temp.push_back(make_pair(nums[i], i));
        sort(temp.begin(), temp.end());
        for (int i = 0; i < n; ++i) {
            int idx = binary_search(temp, i + 1, n - 1, target - temp[i].first);
            if (idx != -1) {//find answer
                ans.push_back(temp[i].second);
                ans.push_back(temp[idx].second);
                return ans;
            }
        }
        return ans;
    }
};
```

