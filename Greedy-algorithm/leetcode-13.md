# LeetCode 13. Roman to Integer  [link](https://leetcode.com/problems/roman-to-integer/)

## Problem description:

> Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.
>
> ```
> Symbol       Value
> I             1
> V             5
> X             10
> L             50
> C             100
> D             500
> M             1000
> ```
>
> For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.
>
> Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:
>
> - `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
> - `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
> - `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.
>
> Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.

## Example:

```
Input: "III"
Output: 3

Input: "IV"
Output: 4

Input: "IX"
Output: 9

Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.

Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Solution:

### Tags:

#### *[Greedy algorithm](https://github.com/yang-233/Algorithm-note/tree/master/Greedy-algorithm)*

### How to do:

> Because roman numerals must be in descending order. We can use this lows to find the "IV" , "IX" etc..

### Code:

```c++
class Solution {
public:
    int getVal(char ch) {
        switch (ch) {
            case 'I':
                return 1;
            case 'V':
                return 5;
            case 'X':
                return 10;
            case 'L':
                return 50;
            case 'C':
                return 100;
            case 'D':
                return 500;
            case 'M':
                return 1000;
            default:
                return 0;
        }
    }

    int romanToInt(string s) {
        int ans = 0, n = s.length();
        for (int i = 0; i < n; i++) {
            ans += getVal(s[i]);
            if (i > 0 && getVal(s[i]) > getVal(s[i - 1]))
                ans -= 2 * getVal(s[i - 1]);
        }
        return ans;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

