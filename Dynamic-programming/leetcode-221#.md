# [LeetCode 221. Maximal Square](https://leetcode.com/problems/maximal-square/)

## Problem description:

> Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

## Example:

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

## Solution:

### Tags:

#### *[Dynamic programming](https://github.com/yang-233/Algorithm-note/tree/master/Dynamic%20planning)* 

### How to do:

> 用一个二维dp数组来记录边长，*dp\[i\]\[j\]*表示以i,j这个位置为右下角的最大正方形的边长。则当*mat\[i\]\[j\]*为1时，更新*dp\[i\]\[j\] = max(dp\[i - 1\]\[j - 1\], dp\[i\]\[j - 1\], dp\[i\]\[j - 1\]) + 1*否则*dp\[i\]\[j\] = 0*.

### Code:

```c++
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        if (matrix.empty() || matrix[0].empty()) 
            return 0;
        int m = matrix.size(), n = matrix[0].size(), res = 0;
        vector<vector<int>> dp(m, vector<int>(n, 0));
        //dp[i][j]表示以mat[i][j]为右下角的最大正方形的边长
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (i == 0 || j == 0) 
                    dp[i][j] = matrix[i][j] - '0';
                else 
                    if (matrix[i][j] == '1') 
                        dp[i][j] = min(dp[i - 1][j - 1], min(dp[i][j - 1], dp[i - 1][j])) + 1;
                
                res = max(res, dp[i][j]);
            }
        }
        return res * res;
    }
};
```

### Time complexity:

#### *O (n^2)*

### Space complexity:

#### *O(n^2)*

