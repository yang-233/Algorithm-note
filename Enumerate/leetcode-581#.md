# [LeetCode 448. Find All Numbers Disappeared in an Array](<https://leetcode.com/problems/shortest-unsorted-continuous-subarray/>) 

## Problem description:

Given an integer array, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the **shortest** such subarray and output its length.

**Note:**

1. Then length of the input array is in range [1, 10,000].
2. The input array may contain duplicates, so ascending order here means **<=**.

> ```
> Input: [2, 6, 4, 8, 10, 9, 15]
> Output: 5
> Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
> ```

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

> If *a[i] < max(a[0]...a[i - 1])*, the i must <= the end of the disorder interval. Similarly, if *a[n - i - i] > min(a[n - i - 1], a[n - 1])*  the i must >= the begin of the disorder interval.

### Code:

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& a) {
        return method2(a);
    }
    
    int method1(const vector<int>& a) {
        vector<int> t = a;
        sort(t.begin(), t.end());
        
        int n = a.size(), l = 0, r = n - 1;
        
        while(l < n && a[l] == t[l]) // l -> n
            ++l;
        while(r > l + 1 && a[r] == t[r]) // r -> l + 1
            --r;
        return r - l + 1;
    }
    
    int method2(const vector<int>& a) {
        int n = a.size(), end = -1, begin = 0;
        int MAX = a[0], MIN = a.back();
        
        for(int i = 0; i < n; ++i) {
            MAX = max(MAX, a[i]);
            if(a[i] < MAX) {
            	end = i;
            	//printf("MAX = %d, l = %d, a[i] = %d\n", MAX, l, a[i]);
			}
            MIN = min(MIN, a[n - i - 1]);
            if(a[n - i - 1] > MIN) {
            	begin = n - i - 1;
            	//printf("MIN = %d, r = %d, a[n - i - 1] = %d\n", MIN, r, a[n - i -1]); 
			}
        }
        return end - begin + 1;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

