# LeetCode 9. Palindrome Number  [link](https://leetcode.com/problems/palindrome-number/)

## Problem description:

> Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

## Example:

```
Input: 121
Output: true

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

## Solution:

### Tags:

#### *[Discover laws](https://github.com/yang-233/Algorithm-note/tree/master/Discover-laws)* 

### How to do:

> Too simple.

### Code:

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0)
            return false;
        int ans = 0, temp = x;
        while (temp) {
            ans = ans * 10 + temp % 10;
            temp /= 10;
        }
        return ans == x;
    }
};
```

### Time complexity:

#### *O (1)*

### Space complexity:

#### *O(1)*

