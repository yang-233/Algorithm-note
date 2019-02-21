# LeetCode 523. Continuous Subarray Sum [link](https://leetcode.com/problems/continuous-subarray-sum/)

## Problem description:

> Given a list of **non-negative** numbers and a target **integer** k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of **k**, that is, sums up to n*k where n is also an **integer**.
>
> **Note:**
>
> 1. The length of the array won't exceed 10,000.
> 2. You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

## Example:

>```
>Input: [23, 2, 4, 6, 7],  k=6
>Output: True
>Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
>
>Input: [23, 2, 6, 4, 7],  k=6
>Output: True
>Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
>```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

### How to do:

> if a[i] + a[i + 1] +...+a[j] = n1 \* k + q and a[i] + a[i + 1] +...+ a[j] + a[j + 1] +...+a[k] = n2 \* k + q  :
>
> a[j + 1] +...+a[k] = (n2 - n1) \* k. Use hash map to record the value -> index. We need to deal with some special situation like this: [0, 0] k = 0. So, we need to insert {0 -> -1}.

### Code:

```c++
class Solution {
public:
    bool checkSubarraySum(vector<int>& a, int k) {
        int sum = 0, res = 0;
        unordered_map<int, int> m;//value -> index
        m[0] = -1;// [0,0] k = 0
        for(int i = 0; i < a.size(); ++i) {
            sum += a[i];
            if(k != 0)
                sum %= k;
            auto ptr = m.find(sum);
            if(ptr != m.end()) {
                if(i - ptr->second > 1)//the gap of index bigger than 1
                    return true;
            }
            else//only save the most small index
                m[sum] = i;
        }
        return false;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

