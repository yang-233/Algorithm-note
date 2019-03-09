# LeetCode 448. Find All Numbers Disappeared in an Array [link](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

## Problem description:

> Given an array of integers where 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear twice and others appear once.
>
> Find all the elements of [1, *n*] inclusive that do not appear in this array.
>
> Could you do it without extra space and in O(*n*) runtime? You may assume the returned list does not count as extra space.

## Example:

>```
>Input:
>[4,3,2,7,8,2,3,1]
>
>Output:
>[5,6]
>```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

#### How to do:

> Because the range of the numbers is [1, n], in that , we can use the sign of the *a[i]* to record the exist of the *i*.

### Code:

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& a) {
        vector<int> res;
        int n = a.size();
        for(int i = 0; i < n; ++i ) {
            int idx = (a[i] > 0 ? a[i] : -a[i]) - 1;
            a[idx] = a[idx] < 0 ? a[idx] : -a[idx];
        }
        
        for(int i = 0; i < n; ++i)
            if(a[i] > 0)
                res.push_back(i + 1);
        return res;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

