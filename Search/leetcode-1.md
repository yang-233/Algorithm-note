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

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)* 

### How to do:

> Use hash table to record every value's index. For each *nums[i]* in *nums*. find the *target - nums[i]* in the hash table. We need to solve a special case that the nums contains repeated value and *nums[i] \* 2 == target*. 

### Code:

```c++
class Solution {
public:
    vector<int> twoSum(vector<int> &nums, int target) {
        vector<int> ans;
        unordered_map<int, vector<int>> m;//value -> indices
        for (auto i: nums)
            m[i] = vector<int>();
        for (int i = 0; i < nums.size(); ++i)
            m[nums[i]].push_back(i);
        for (auto i : nums) {
            if (m.find(target - i) != m.end()) {
                if(i == target - i){
                    if(m[i].size() > 1){
                        ans.push_back(m[i][0]);
                        ans.push_back(m[i][1]);
                        break;
                    }
                }
                else{
                    ans.push_back(m[i][0]);
                    ans.push_back(m[target - i][0]);
                    break;
                }
            }
        }
        return ans;
    }
};
```

### Time complexity:

#### *O(n)*

### Space complexity:

#### *O(n)*