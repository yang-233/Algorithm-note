# LeetCode 5. Longest Palindromic Substring[link](https://leetcode.com/problems/longest-palindromic-substring/)

## Problem description:

> Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

## Example:

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Input: "cbbd"
Output: "bb"
```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/%20Enumerate)*    *[Dynamic planning](https://github.com/yang-233/Algorithm-note/tree/master/Dynamic%20planning)* 

### How to do:

> Inspired by [this article](https://blog.csdn.net/camellhf/article/details/70663406), [this article](https://subetter.com/articles/manacher-algorithm.html).

### Code:

```c++
class Solution {
public:
    string init(string s) {
        string ans(s.length() * 2 + 3, '#');
        ans[0] = '$';
        for (int i = 0, j = 2; i < s.length(); i++, j += 2)
            ans[j] = s[i];
        ans.back() = '\0';
        return ans;
    }

    pair<int, int> manacher(string s) {
        s = init(s);
        int max_len = 0,//the length of the current longest palindromic substring.
                right = 0,//the right end of the longest palindromic substring.
                start = 0,//the longest palindromic substring's beginning
                mid;//the mid of the current longest palindromic substring.
        int *p = new int[s.length()];//p[i] the radius of the longest palindrome substring centered on i.
        for (int i = 1; i < s.length(); i++) {
            if (i < right)
                p[i] = min(p[2 * mid - i],//2 * mid - i is the symmetric point of i
                           right - i);
            else
                p[i] = 1;
            while (s[i - p[i]] == s[i + p[i]])
                p[i]++;
            if (right < i + p[i]) {
                mid = i;
                right = i + p[i];
            }
            if (p[i] - 1 > max_len) {
                max_len = p[i] - 1;
                start = (i - p[i]) / 2;//because i is the longest
                //palindromic substring's right end
            }
            max_len = max(max_len, p[i] - 1);
        }
        return {start, max_len};
    }

    pair<int, int> dp(const string &s) {
        int n = s.length();
        int start = 0, max_len = 1;
        vector<vector<bool>> dp(n, vector<bool>(n, false));

        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            if (i + 1 < n && s[i] == s[i + 1]) {
                dp[i][i + 1] = true;
                start = i;
                max_len = 2;
            }

        }

        for (int i = n - 1; i >= 0; i--) {
            for (int j = i + 2; j < n; j++) {
                if (dp[i + 1][j - 1] && s[i] == s[j]) {
                    dp[i][j] = true;
                    if (j - i + 1 > max_len) {
                        start = i;
                        max_len = j - i + 1;
                    }
                }
            }
        }
        return {start, max_len};
    }

    string longestPalindrome(string s) {
        pair<int, int> ans = dp(s);//manacher(s);
        return s.substr(ans.first, ans.second);
    }
};
```

### Time complexity:

#### DP : *O(n^2)* Manacher : *O (n)*

### Space complexity:

#### DP : * O(n)* Manacher : *O(n)*

