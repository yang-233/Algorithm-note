# LeetCode 567. Permutation in String	 [link](https://leetcode.com/problems/permutation-in-string/)

## Problem description:

> Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.
>
> **Note:**
>
> 1. The input strings only contain lower case letters.
> 2. The length of both given strings is in range [1, 10,000].

## Example:

```
Input:s1 = "ab" s2 = "eidbaooo"
Output:True
Explanation: s2 contains one permutation of s1 ("ba").

Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)*

### How to do:

> Use the sliding window approach. And we will find that the legal window's length is fixed.

### Code:

```c++
class Solution {
public:
    static const int M = 26;

    bool checkInclusion(string s1, string s2) {
        if(s1.empty() || s2.empty())
            return false;
        int num[M] = {0};
        for (char i: s1)
            ++num[i - 'a'];
        for (int l = 0, r = 0, curNum[M] = {0}; r < s2.length(); ++r) {
            int t = s2[r] - 'a';
            ++curNum[t];
            if (num[t]) {
                if (curNum[t] > num[t]) {
                    for (int i = l;; ++i) {
                        --curNum[s2[i] - 'a'];
                        if (s2[i] == s2[r]) {
                            l = i + 1;
                            break;
                        }
                    }
                }
                if (r - l + 1 == s1.length())
                    return true;
            } else {
                fill(curNum, curNum + M, 0);
                l = r + 1;
            }
        }
        return false;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

