# LeetCode 90. Subsets II [link](https://leetcode.com/problems/subsets-ii/)

## Problem description:

> Given a collection of integers that might contain duplicates, **nums**, return all possible subsets (the power set).
>
> **Note:** The solution set must not contain duplicate subsets.

## Example:

>```
>Input: [1,2,2]
>Output:
>[
>  [2],
>  [1],
>  [1,2,2],
>  [2,2],
>  [1,2],
>  []
>]
>```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

### How to do:

> Because when we don't select the a[a.size() - 1] , we can't go to the state that idx == a.size(). 

### Code:

```c++
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& a) {
        sort(a.begin(), a.end());
        
        vector<int> ans;
        vector<vector<int>> res;
        dfs(a, 0, ans, res);
        return res;
    }
    void dfs(const vector<int>& a, int idx, vector<int>& ans, vector<vector<int>>& res) {
        res.push_back(ans);
        for(int i = idx; i < a.size(); ++i) {
            if(i > idx && a[i] == a[i - 1])
                continue;
            ans.push_back(a[i]);
            dfs(a, i + 1, ans, res);
            ans.pop_back();
        }
    }
};

```

### Time complexity:

#### *O (2^n)*

### Space complexity:

#### *O(n)*

