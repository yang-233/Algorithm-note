# [leetcode - 240. 搜索二维矩阵 II](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)

## 题目描述:

编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

* 每行的元素从左到右升序排列。
* 每列的元素从上到下升序排列。

> ```
> [
>   [1,   4,  7, 11, 15],
>   [2,   5,  8, 12, 19],
>   [3,   6,  9, 16, 22],
>   [10, 13, 14, 17, 24],
>   [18, 21, 23, 26, 30]
> ]
> 给定 target = 5，返回 true。
> 
> 给定 target = 20，返回 false。
> ```

## 题解:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

#### 怎么做:

> 从右上角开始搜索，小了往左移，大了往下移。

### Code:

```c++
class Solution {
public:

    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.size() == 0 || matrix[0].size() == 0)
            return false;
        int i = 0, j = matrix[0].size() - 1;
        while(i < matrix.size() && j >= 0) {
            if(matrix[i][j] == target)
                return true;
            else if(matrix[i][j] > target)
                --j;
            else
                ++i;
        }
        return false;
    }
};
```

### Time complexity:

#### *O (m + n)*

### Space complexity:

#### *O(m\*n)*

