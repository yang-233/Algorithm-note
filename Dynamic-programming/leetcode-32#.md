# LeetCode 32. Longest Valid Parentheses	 [link](https://leetcode.com/problems/longest-valid-parentheses/)

## Problem description:

> Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

## Example:

```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"

Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"

```

## Solution:

### Tags:

#### *[Dynamic programming](https://github.com/yang-233/Algorithm-note/tree/master/Dynamic%20planning)* 

### How to do:

> Use *dynamic programming approach*. *dp[i]* denote that the length of the max valid parentheses ending with *i*(it means that *s[i]* must be ')' ). Then, we just need to handing two situation. First, s[i - 1] was '(' : *dp[i] = dp[i - 2] + 2*. Second, *if s[i - 1] = ')'  and s[i - 1 - dp[i - 1]] == '(': dp[i] = dp[i - 1] + 2 +dp[i - 1 -dp[i - 1] - 1]*.
>
> (if dp[i - 1] == 0 : i - 1 - dp[i - 1] == i - 1)

### Code:

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        vector<int> dp(s.length(), 0);
        int ans = 0;
        for(int i = 1; i < s.length(); ++i) {
            if(s[i] == ')') {
                if(s[i - 1] == '(') 
                    dp[i] = 2 + ((i >= 2)? dp[i - 2] : 0); 
                else if(s[i - 1 - dp[i - 1]] == '(')
                    dp[i] = dp[i - 1] + 2 + 
                    ((i - 1 - dp[i - 1] - 1 >= 0) ? 
                     dp[i - 1 - dp[i - 1] - 1] : 0); 
            }
            ans = max(ans, dp[i]);
        }
        return ans;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

