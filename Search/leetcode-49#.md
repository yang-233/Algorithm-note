# LeetCode 49. Group Anagrams Arrays [link](https://leetcode.com/problems/group-anagrams/)

## Problem description:

> Given an array of strings, group anagrams together.

## Example:

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

#### Note:

>- All inputs will be in lowercase.
>- The order of your output does not matter.

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)* 

### How to do:

> Use sort and hash table.

### Code:

```c++
class Solution {
public:
    
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        unordered_map<string, int> m;
        int idx = 0;
        for(auto i : strs) {
            string t = i;
            sort(t.begin(), t.end());
            auto ptr = m.find(t);
            if(ptr == m.end()) {
                m[t] = idx++;
                res.push_back(vector<string>());
            } 
            res[m[t]].push_back(i);
        }
        return res;
    }
};
```

### Time complexity:

#### *O(n\*log(n))*

### Space complexity:

#### *O(n)*

