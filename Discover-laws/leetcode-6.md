# LeetCode 6. ZigZag Conversion [link](https://leetcode.com/problems/zigzag-conversion/)

## Problem description:

> The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
>
> ```
> P   A   H   N
> A P L S I I G
> Y   I   R
> ```
>
> And then read line by line: `"PAHNAPLSIIGYIR"`
>
> Write the code that will take a string and make this conversion given a number of rows:
>
> ```
> string convert(string s, int numRows);
> ```

## Example:

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
Explanation:
P   A   H   N
A P L S I I G
Y   I   R

Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
```

## Solution:

### Tags:

#### *[Discover laws](https://github.com/yang-233/Algorithm-note/tree/master/Discover-laws)* 

### How to do:

> In one circle, there are up to two characters per line. 

### Code:

```c++
class Solution {
public:
    string convert(string s, int numRows) {
        if(numRows == 1)//if numRows == 1, T = 0;
            return s;
        const int T = numRows * 2 - 2;
        int n = s.length();
        string ans;
        for (int i = 0; i < numRows; i++) {
            for (int j = i; j < n; j += T) {
                ans += s[j];
                if (i > 0 && i < numRows - 1 && (j + T - 2 * i) < n) {
                    ans += s[j + T - 2 * i];
                }
            }
        }
        return ans;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

