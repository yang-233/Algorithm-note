# [Leetcode 41. 缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)

## Problem description:

#### Example:

>```
>输入: [1,2,0]
>输出: 3
>
>输入: [3,4,-1,1]
>输出: 2
>
>输入: [7,8,9,11,12]
>输出: 1
>```

**提示：**

你的算法的时间复杂度应为O(*n*)，并且只能使用常数级别的额外空间。

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

#### How to do:

> 用数组中[0, n)这个这些下标对应的数的正负来代表1-n这些数字是否出现了，一开始需要将所有小于等于0的数初始化为一个较大的整数，某数字出现后，将该数字作为下表对应的那个数置为负数，考虑到会有重复的数，还需要判定该位置上的数字大于0时再处理。注意处理边界，比如

### Code:

```c++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        for(int i = 0; i < n; i++) {//将所有非正数变为一个大于数组区间的数
            if(nums[i] <= 0)
                nums[i] = 1e9;    
        }
        for(int i = 0; i < n; i++) {
            int t = abs(nums[i]);//某些位置可能已经被置为负数了
            if(t > 0 && t <= n && nums[t - 1] > 0)//需要判定是否大于0，否则多次出现的数正负性无法确定
                nums[t - 1] = -nums[t - 1];
        }
        for(int i = 0; i < n; ++i) {
            if(nums[i] > 0)//[0, n-1] -> [1, n]
                return i + 1;
        }
        return n + 1;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

