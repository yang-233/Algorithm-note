# LeetCode 14. Longest Common Prefix  [link](https://leetcode.com/problems/longest-common-prefix/)

## Problem description:

> Write a function to find the longest common prefix string amongst an array of strings.
>
> If there is no common prefix, return an empty string `""`.
>
>

## Example:

```
Input: ["flower","flow","flight"]
Output: "fl"

Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/%20Enumerate)* 

### How to do:

> Use an array to record the number of occurrences of each character in each position. And then check the characters that appear n times in each position.

### Code:

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string> &strs) {
        vector<vector<int>> v;
        const int M = 26;
        string ans;
        int n = strs.size();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < strs[i].length(); j++) {
                if (j + 1 > v.size())
                    v.push_back(vector<int>(M, 0));
                v[j][strs[i][j] - 'a']++;
            }
        }
        for (int i = 0; i < v.size(); i++) {
            bool find = false;
            for (int j = 0; j < M; j++) {
                if (v[i][j] == n) {
                    find = true;
                    ans += 'a' + j;
                    break;
                }
            }
            if (!find)
                break;
        }
        return ans;
    }
};
```

### Time complexity:

#### *O (max_lenngth)*

### Space complexity:

#### *O(max_length)*

