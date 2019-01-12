# LeetCode 17. Letter Combinations of a Phone Number  [link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

## Problem description:

> Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.
>
> A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
>
> ![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

## Example:

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/%20Enumerate)* 

### How to do:

> Use dfs approach.

### Code:

```c++
class Solution {
public:
    void dfs(vector<string> &ans, char m[][5], const string &d, int len, vector<char> &t) {
        if (len >= d.length()) {
            if (!t.empty())
            	ans.push_back(string(t.begin(), t.end()));
            return;
        }
        for (int i = 0; m[d[len] - '0' - 1][i]; ++i) {
            t.push_back(m[d[len] - '0' - 1][i]);
            dfs(ans, m, d, len + 1, t);
            t.pop_back();
        }
    }

    vector<string> letterCombinations(string digits) {
        char m[][5] = {
                "",
                "abc",
                "def",
                "ghi",
                "jkl",
                "mno",
                "pqrs",
                "tuv",
                "wxyz"
        };
        vector<string> ans;
        vector<char> t;
        dfs(ans, m, digits, 0, t);
        return ans;
    }
};
```

### Time complexity:

#### *O (5^len(digits))*

### Space complexity:

#### *O(1)*

