# LeetCode 15. 3Sum  [link](https://leetcode.com/problems/3sum/)

## Problem description:

> Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.
>
> **Note:**
>
> The solution set must not contain duplicate triplets.

## Example:

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)* 

### How to do:

> The key is to eliminate duplication. And the two pointer approach has better efficiency.

### Code:

```c++
class Solution {
public:
    int binarySearch(const vector<int> &a, int l, int r, int val) {
        while (l <= r) {
            int mid = (l + r) / 2;
            if (a[mid] == val)
                return mid;
            else {
                if (a[mid] > val)
                    r = mid - 1;
                else
                    l = mid + 1;
            }
        }
        return -1;
    }

    vector<vector<int>> binSearch(vector<int> &a) {
        vector<vector<int>> ans;
        int n = a.size();
        sort(a.begin(), a.end());
        for (int i = 0; i < n - 2; i++) {
            if (i && a[i] == a[i - 1])
                continue;
            for (int j = i + 1; j < n - 1; j++) {
                if (j > i + 1 && a[j] == a[j - 1])
                    continue;
                int idx = binarySearch(a, j + 1, n - 1, 0 - a[i] - a[j]);
                if (idx >= 0) {
                    vector<int> temp;
                    temp.push_back(a[i]);
                    temp.push_back(a[j]);
                    temp.push_back(a[idx]);
                    ans.push_back(temp);
                }
            }
        }
        return ans;
    }

    vector<vector<int>> twoPointer(vector<int> &a) {
        int n = a.size();
        vector<vector<int>> ans;
        sort(a.begin(), a.end());
        for (int i = 0; i < n - 2; i++) {
            if (i && a[i] == a[i - 1])
                continue;
            int l = i + 1, r = n - 1;
            while (l < r) {
                while (l > i + 1 && a[l] == a[l - 1])
                    l++;
                if (l >= r)
                    break;
                int t = a[i] + a[l] + a[r];
                if (!t) {
                    vector<int> temp;
                    temp.push_back(a[i]);
                    temp.push_back(a[l]);
                    temp.push_back(a[r]);
                    ans.push_back(temp);
                    l++;
                    r--;
                } else {
                    if (t > 0)
                        r--;
                    else
                        l++;
                }
            }
        }
        return ans;
    }

    vector<vector<int>> threeSum(vector<int> &nums) {
        return twoPointer(nums);
    }
};
```

### Time complexity:

#### *O (n^2)*

### Space complexity:

#### *O(n)*

