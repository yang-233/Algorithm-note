# LeetCode 11. Container With Most Water  [link](https://leetcode.com/problems/container-with-most-water/)

## Problem description:

> Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i*is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
>
> **Note:** You may not slant the container and *n* is at least 2.
>
> ![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)
>
> The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

## Example:

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

## Solution:

### Tags:

#### *[Greedy algorithm](https://github.com/yang-233/Algorithm-note/tree/master/Greedy-algorithm)*

### How to do:

> This is an optimal interval problem. We define the left( initial value = 0) and right pointers( initial value= n - 1), then continue to narrow the interval. How to narrow? Obviously, narrow the smaller side of the height gives you a better chance of getting a better solution. For each group interval, it's answer is *min(height[l], height[r]) \* (r - l)*

### Code:

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int l = 0, r = height.size() - 1;
        long long ans = 0;
        while (l < r) {
            ans = max(ans, (long long)min(height[l], height[r]) * (r - l));
            if(height[l] < height[r])//Move the lower side endpoint.
                l++;
            else
                r--;
        }
        return ans;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

