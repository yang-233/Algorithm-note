# LeetCode 29. Divide Two Integers [link](https://leetcode.com/problems/divide-two-integers/)

## Problem description:

> Given two integers `dividend` and `divisor`, divide two integers without using multiplication, division and mod operator.
>
> Return the quotient after dividing `dividend` by `divisor`.
>
> The integer division should truncate toward zero.
>
> **Note:**
>
> - Both dividend and divisor will be 32-bit signed integers.
> - The divisor will never be 0.
> - Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 2^31 − 1 when the division result overflows.

## Example:

```
Input: dividend = 10, divisor = 3
Output: 3

Input: dividend = 7, divisor = -3
Output: -2
```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

### How to do:

> Use the power of 2 to optimize th approach.

### Code:

```c++
class Solution {
public:
    int divide(int dividend, int divisor) {
        if(dividend == INT_MIN && divisor == -1)
            return INT_MAX;
        bool sign = (dividend > 0) ^ (divisor > 0);
        long long a = labs(dividend), b = labs(divisor);
        int result = 0;
        while(a >= b) {
            long long temp = b;
            int power = 1;
            while(a >= (temp << 1)) {
                power <<= 1;
                temp <<= 1;
            } 
            a -= temp;
            result += power;
        }
        return sign ? -result : result;
    }
};
```

### Time complexity:

#### *O (log(n))*

### Space complexity:

#### *O(1)*

