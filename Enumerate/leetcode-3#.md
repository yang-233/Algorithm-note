# LeetCode 3. Longest Substring Without Repeating Characters [link](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

## Problem description:

> Given a string, find the length of the **longest substring** without repeating characters.

## Example:

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not 				a substring.
```

## Solution:

### Tag:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/%20Enumerate)* 

### How to do:

> Take the *"Sliding window approach"*. Use a boolean array to record what chars in current substring.

### Code:

```c++
class Solution {
public:
    const int N = 1 << (sizeof(char) * 8);

    int lengthOfLongestSubstring(string s) {
        int ans = 0;
        bool ch[N];
        fill(ch, ch + N, false);
        for (int l = 0, r = 0; r < s.size(); ++r) {
            if (!ch[s[r]]) {//The char has not yet appeared.
                ch[s[r]] = true;
                ans = max(ans, r - l + 1);
            } else {//Fixed the right endpoint and move the left endpoint.
                while (l < r) {
                    if (s[l] != s[r])
                        ch[s[l]] = false;
                    else//Find the repetitive char.
                        break;
                    ++l;
                }
                ++l;
            }
        }
        return ans;
    }
};
```

### Time complexity:

#### *O(n)*

### Space complexity:

#### *O(n)*

