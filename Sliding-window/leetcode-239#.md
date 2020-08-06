# LeetCode 239. [滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/) 

## Problem description:

> 给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。
>
> 返回滑动窗口中的最大值。
>
> **进阶：**
>
> 你能在线性时间复杂度内解决此题吗？

## Example:

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**提示：**

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

## Solution:

### Tags:

#### *[Greedy-algorithm](https://github.com/yang-233/Algorithm-note/tree/master/Sliding-window)*

### How to do:

> 用单调不增的双向队列来维护滑窗。队首永远是最大值，每个值至多进出队列一次，O(n)

### Code:

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        return OnSolution(nums, k);
        // multiset<int> s;// 不能保证数组中没有重合元素，应该使用multiset
        // vector<int> res;
        // int i = 0;
        // for(; i < k - 1 && i < nums.size(); ++i) // 先插入k-1个数
        //     s.insert(nums[i]);
        // do {
        //     s.insert(nums[i]); // 插入一个新数值
        //     res.push_back(*s.rbegin()); // 获取堆中最大值，即集合中最后一个元素
        //     s.erase(s.find(nums[i - k + 1])); // 删除掉最左侧的值
        //     ++i; // 窗口滑动
        // } while(i < nums.size());
        // return res;
    }

    //用一个单调不增队列来维护滑动窗口，队首永远是最大值，每个元素至多进出队列一次，复杂度为O（N）
    vector<int> OnSolution(vector<int>& a, int k) {
        deque<int> window; // 用于维护整个window中数字的下标
        vector<int> res;
        for(int i = 0; i < a.size(); ++i) {
            if(!window.empty() && i - window[0] >= k)//检查最大元素是否还在窗口中
                window.pop_front();
            while(!window.empty() && a[window.back()] < a[i]) // 窗口中比a[i]小的数都弹出去
                window.pop_back();
            window.push_back(i);
            if(i >= k - 1)
                res.push_back(a[window[0]]);//把当前窗口中最大的元素加入结果中
        }
        return res;
    }
};
```

### Time complexity:

#### *O(n)*

### Space complexity:

#### *O(n)*

