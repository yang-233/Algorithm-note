# LeetCode 28. Implement strStr() [link](https://leetcode.com/problems/implement-strstr/)

## Problem description:

> Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).
>
> Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.
>
> **Clarification:**
>
> What should we return when `needle` is an empty string? This is a great question to ask during an interview.
>
> For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

## Example:

```
Input: haystack = "hello", needle = "ll"
Output: 2

Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

## Solution:

### Tags:

#### *[Dynamic programming](https://github.com/yang-233/Algorithm-note/tree/master/Dynamic%20planning)* 

### How to do:

> Use *kmp* algorithm. Use Dynamic programming idea to understand the next array.
>
> *[This blog](https://www.cnblogs.com/haolujun/archive/2012/10/17/2728015.html)*.

### Code:

```c++
class Solution {
public:
    int* get_nextval(const char *str) {
        int i = 0, j = -1;
        int *nextval = new int[strlen(str) + 1];
        nextval[0] = -1;
        while (str[i]) {
            if (j == -1 || str[i] == str[j]) {
                ++i;
                ++j;
                if (str[i] == str[j])
                    nextval[i] = nextval[j];
                else
                    nextval[i] = j;
            } else
                j = nextval[j];
        }
        return nextval;
    }
    int kmp(const char *str, const char *sub) {
        int m = strlen(str), n = strlen(sub);
        int i = 0, j = 0;
        int *nextval = get_nextval(sub);
        while (i < m && j < n) {
            if (j == -1 || str[i] == sub[j]) {
                ++i;
                ++j;
            } else
                j = nextval[j];
        }
        return j == n ? i - n : -1;
    }
    int strStr(string haystack, string needle) {
        return kmp(haystack.c_str(), needle.c_str());
    }
};
```

### Time complexity:

#### *O (m+n)*

### Space complexity:

#### *O(n)*

