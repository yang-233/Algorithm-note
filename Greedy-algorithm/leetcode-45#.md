# [LeetCode 45. Jump Game II](<https://leetcode.com/problems/jump-game-ii/>) 

## Problem description:

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

**Note:**

You can assume that you can always reach the last index.

## Example:

>```
>Input: [2,3,1,1,4]
>Output: 2
>Explanation: The minimum number of jumps to reach the last index is 2.
>    Jump 1 step from index 0 to 1, then 3 steps to the last index.
>```

## Solution:

### Tags:

#### *[Greedy-algorithm](https://github.com/yang-233/Algorithm-note/tree/master/Greedy-algorithm)*

#### How to do:

> This problem can be solved using a greedy algorithm. 
>
> 1. *step* is used to to record the number of step.
> 2. *lastPos* is used to record the maximum position that can be reached after step *step*.
> 3. *maxPos*  is used to record the maximum position that can be reached when processing to the *i* th position. 
> 4. If *i > lastPos* then *step = step + 1* and *lastPos = maxPos*.

### Code:

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int step = 0, maxPos = 0, lastPos = 0;
        for(int i = 0; i < nums.size(); ++i) {
            if(i > lastPos) {//this i can not be reach from lastPos
                ++step;//so we should move a step
                lastPos = maxPos;
            }
            maxPos = max(maxPos, i + nums[i]);
            //The number of steps required to reach [0, maxPos] 
            //must be less than or equal to step
        }
        return step;
    }        
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

