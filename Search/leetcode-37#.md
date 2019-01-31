# LeetCode 37. Sudoku Solver [link](https://leetcode.com/problems/sudoku-solver/)

## Problem description:

> Write a program to solve a Sudoku puzzle by filling the empty cells.
>
> A sudoku solution must satisfy **all of the following rules**:
>
> 1. Each of the digits `1-9` must occur exactly once in each row.
> 2. Each of the digits `1-9` must occur exactly once in each column.
> 3. Each of the the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.
>
> Empty cells are indicated by the character `'.'`.
>
> **Note:**
>
> - The given board contain only digits `1-9` and the character `'.'`.
> - You may assume that the given Sudoku puzzle will have a single unique solution.
> - The given board size is always `9x9`.

## Example:

>![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
>
>A sudoku puzzle...
>
>![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)
>
>...and its solution numbers marked in red.

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)*

### How to do:

> Use dfs.

### Code:

```c++
class Solution {
public:
    bool flag;
    vector<int> count(vector<vector<char>>& m, int i, int j) {
        bool num[10];
        vector<int> ans;
        fill(num, num + 10, false);
        for(int k = 0; k < 9; ++k) {
            if(m[i][k] != '.')
                num[m[i][k] - '0'] = true;
            if(m[k][j] != '.')
                num[m[k][j] - '0'] = true;
        }
        for(int p = i - i % 3, q = j - j % 3, x = 0; x < 3; ++x)
            for(int y = 0; y < 3; ++y)
                if(m[p + x][q + y] != '.')
                    num[m[p + x][q + y] - '0'] = true;
        for(int i = 1; i < 10; ++i)
            if(!num[i])
                ans.push_back(i);
        return ans;
    }

    pair<int, int> nextIdx(const vector<vector<char>>& m, int i, int j) {
        for(; j < 9; ++j)
            if(m[i][j] == '.')
                return {i, j};
        for(++i; i < 9; ++i)
            for(j = 0; j < 9; ++j)
                if(m[i][j] == '.')
                    return {i, j};
        return {-1,-1}; //end
    }

    void dfs(vector<vector<char>>& m, int i, int j) {
        pair<int, int> idx = nextIdx(m, i, j);
        if(idx.first == -1)
            flag = true;
        if(flag)
            return;
        vector<int> num = count(m, idx.first, idx.second);
        for(int val : num) {
            m[idx.first][idx.second] = '0' + val;
            dfs(m, idx.first, idx.second);
            if(flag)
                return;
            m[idx.first][idx.second] = '.';
        }
    }
    
    void solveSudoku(vector<vector<char>>& m) {
        flag = false;
        dfs(m, 0, 0);
    }
};
```

### Time complexity:

#### ?

### Space complexity:

#### *O(1)*

