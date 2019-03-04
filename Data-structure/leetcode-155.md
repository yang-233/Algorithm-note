# LeetCode 155. Min Stack [link](https://leetcode.com/problems/min-stack/)

## Problem description:

> Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
>
> - push(x) -- Push element x onto stack.
> - pop() -- Removes the element on top of the stack.
> - top() -- Get the top element.
> - getMin() -- Retrieve the minimum element in the stack.

## Example:

>```
>MinStack minStack = new MinStack();
>minStack.push(-2);
>minStack.push(0);
>minStack.push(-3);
>minStack.getMin();   --> Returns -3.
>minStack.pop();
>minStack.top();      --> Returns 0.
>minStack.getMin();   --> Returns -2.
>```

## Solution:

### Tags:

#### *[Data Structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Use an extra stack to store val( the val in the extra stack is descending order). So, the min stack's values  
>
> is the subset of the  main stack.

### Code:

```c++
class MinStack {
    stack<int> st, mst;
public:
    /** initialize your data structure here. */
    MinStack() {

    }
    
    void push(int x) {
        st.push(x);
        if(mst.empty() || x <= mst.top())
            mst.push(x);
    }
    
    void pop() {
        if(st.top() == mst.top())
            mst.pop();
        st.pop();
    }
    
    int top() {
        return st.top();
    }
    
    int getMin() {
        return mst.top();
    }
};
```

### Time complexity:

#### *O (1)*

### Space complexity:

#### *O(n)*

