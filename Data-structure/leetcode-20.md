# LeetCode 20. Valid Parentheses [link](https://leetcode.com/problems/valid-parentheses/)

## Problem description:

> Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.
>
> An input string is valid if:
>
> 1. Open brackets must be closed by the same type of brackets.
> 2. Open brackets must be closed in the correct order.
>
> Note that an empty string is also considered valid.

## Example:

```
Input: "()"
Output: true

Input: "()[]{}"
Output: true

Input: "(]"
Output: false

Input: "([)]"
Output: false

Input: "{[]}"
Output: true
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Use stack.

### Code:

```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (char ch: s) {
            if (!st.empty() && ((ch == ')' && st.top() == '(') ||
                                (ch == ']' && st.top() == '[') ||
                                (ch == '}' && st.top() == '{')))
                st.pop();
            else
                st.push(ch);
        }
        return st.empty();
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(n)*

