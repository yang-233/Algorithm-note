# LeetCode 31. Next Permutation	 [link](https://leetcode.com/problems/next-permutation/)

## Problem description:

> 1. Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.
>
>    If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
>
>    The replacement must be **in-place** and use only constant extra memory.
>
>    Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
>
>    

## Example:

```
1,2,3 -> 1,3,2
3,2,1 -> 1,2,3
1,1,5 -> 1,5,1
```

## Solution:

### Tags:

#### *[Discover laws](https://github.com/yang-233/Algorithm-note/tree/master/Discover-laws)* 

### How to do:

> Find the first reverse order element *a[i]* from the back to the front. And then find the min element that bigger than *a[i]*. And then sort *a[i + 1, n - 1]*. If the permutation is the last permutation, sort the entire array.

### Code:

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        if(nums.size() < 2)
            return;
        int len = nums.size();
        int idx = 0, MIN = 0;
        bool find = false;
        for(int i = len - 2; i >= 0; --i)
            if(nums[i] < nums[i + 1]) {
                idx = i;
                find = true;
                break;
            }
        MIN = idx + 1;
        for(int i = idx + 2; i < len; ++i)
            if(nums[i] > nums[idx] && nums[i] < nums[MIN])
                MIN = i;
        swap(nums[idx], nums[MIN]);
        if(find)
            sort(nums.begin() + idx + 1, nums.end());
        else
            sort(nums.begin(), nums.end());
    }
};
```

### Time complexity:

#### *O (n\*logn(n))*

### Space complexity:

#### *O(1)*

