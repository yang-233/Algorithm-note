# LeetCode 7. Reverse Integer [link](https://leetcode.com/problems/reverse-integer/)

## Problem description:

> Given a 32-bit signed integer, reverse digits of an integer.

## Example:

```
Input: 123
Output: 321

Input: -123
Output: -321

Input: 120
Output: 21
```

## Solution:

### Tags:

#### *[Discover laws](https://github.com/yang-233/Algorithm-note/tree/master/Discover-laws)* 

### How to do:

> Too simple. We need to deal with a special situation that the *ans* is too big or too small than *INT_MAX*  or *INT_MIN*.

### Code:

```c++
class Solution {
public:
    int reverse(int x) {
        long long ans = 0;
        int temp = abs(x);
        while (temp) {
            ans = ans * 10 + temp % 10;
            temp /= 10;
        }
        if(x < 0)
            ans = -ans;
        if(ans > INT_MAX || ans < INT_MIN)
            return 0;
        return ans;
    }
};
```

### Time complexity:

#### *O (1)*

### Space complexity:

#### *O(1)*

