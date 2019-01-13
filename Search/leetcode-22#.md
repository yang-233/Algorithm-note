# LeetCode 22. Generate Parentheses [link](https://leetcode.com/problems/merge-two-sorted-lists/)

## Problem description:

> Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
>
> For example, given *n* = 3, a solution set is:

## Example:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## Solution:

### Tags:

### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)* 

### How to do:

> A well-formed parentheses must satisfy one condition that it's number of *'('* must more than the number of *')'*. Use this condition to optimize *dfs*. 

### Code:

```c++
class Solution {
public:
    
    void dfs(int n, int l, int r, vector<char> &s, vector<string> &ans) {
        if(l < r)
            return;
        if(l == n && r == n){
            ans.push_back(string(s.begin(), s.end()));
            return;
        }
        if(l < n) {
            s.push_back('(');
            dfs(n, l + 1, r, s, ans);
            s.pop_back();
        }
        if(r < n) {
            s.push_back(')');
            dfs(n, l, r + 1, s, ans);
            s.pop_back();
        }
    }
    
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        vector<char> s;
        dfs(n, 0, 0, s, ans);
        return ans;
    }
};
```

### Time complexity:

#### *O (2^n)*

### Space complexity:

#### *O(n)*

