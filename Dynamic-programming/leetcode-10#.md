# LeetCode 10. Regular Expression Matching [link](https://leetcode.com/problems/regular-expression-matching/)

## Problem description:

> Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'`.
>
> ```
> '.' Matches any single character.
> '*' Matches zero or more of the preceding element.
> ```
>
> The matching should cover the **entire** input string (not partial).
>
> **Note:**
>
> - `s` could be empty and contains only lowercase letters `a-z`.
> - `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

## Example:

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".

Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

## Solution:

### Tags:

#### *[Dynamic programming](https://github.com/yang-233/Algorithm-note/tree/master/Dynamic%20planning)* 

### How to do:

> Inspired by [this blog](https://blog.csdn.net/hk2291976/article/details/51165010).
>
>

### Code:

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        return dp(s,p);
        int n = s.length(), m = p.length();
        vector<vector<int>> t(n, vector<int>(m, -1));
        return match(s, n - 1, p, m - 1, t);
    }

    bool match(const string &s, int i, const string &p, int j, vector<vector<int>> &t) {
        if (j < 0)//If the pattern string has been used up.
            return i < 0;//If the main string also has been used up, return true.
        if (i >= 0 && t[i][j] != -1)//If this result has been calculated, return the result.
            return t[i][j];
        if (p[j] == '*') {
            if (i >= 0 && (p[j - 1] == '.' || p[j - 1] == s[i])) {
                if (match(s, i - 1, p, j, t))//greedy match
                    return t[i][j] = true;
            }
            bool ans = match(s, i, p, j - 2, t);//Backtracking
            if (i >= 0)
                t[i][j] = ans;
            return ans;
        }
        if (i >= 0 && p[j] == '.' || p[j] == s[i])
            return t[i][j] = match(s, i - 1, p, j - 1, t);
        if (i >= 0)
            t[i][j] = false;
        return false;
    }

    bool dp(const string &s, const string &p) {
        int n = s.length(), m = p.length();
        vector<vector<bool>> dp(n + 1, vector<bool>(m + 1, false));//initialize to false
        dp[0][0] = true;//empty string and empty string can be matched.
        for (int j = 2; j <= m; j++)
            dp[0][j] = p[j - 1] == '*' && dp[0][j - 2];//ignore * and the previous char
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= m; j++) {
                if (p[j - 1] == '*')
                    dp[i][j] = dp[i][j - 2] ||//ignore * and the previous char
                               ((s[i - 1] == p[j - 2] || p[j - 2] == '.') && dp[i - 1][j]);//greedy match.
                else//the current character matches successfully.
                    dp[i][j] = (s[i - 1] == p[j - 1] || p[j - 1] == '.') && dp[i - 1][j - 1];
            }
        return dp[n][m];
    }
};
```

### Time complexity:

#### *O (n\*m)*

### Space complexity:

#### *O(n\*m)*

