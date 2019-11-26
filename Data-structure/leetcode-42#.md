# LeetCode  42. Trapping Rain Water  [link]( https://leetcode.com/problems/trapping-rain-water/ )

## Problem description:

>  Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining. 

>The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image! 

## Example:

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Use a stack to find all pit. 

### Code:

```c++
class Solution {
public:
    int trap(vector<int>& h) {
        int res = 0;
        stack<int> st;
        for(int i = 0; i < h.size();) {
            if(st.empty() || h[i] <= h[st.top()])
                st.push(i++);
            else {
                int t = st.top();
                st.pop();
                if(st.empty())
                    continue;
                res += (min(h[i], h[st.top()]) - h[t]) * (i - st.top() - 1);
            }
        }
        return res;
    }

};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

