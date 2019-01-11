# LeetCode 12. Integer to Roman  [link](https://leetcode.com/problems/integer-to-roman/)

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
nput: 3
Output: "III"

Input: 4
Output: "IV"

Input: 9
Output: "IX"

Input: 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

## Solution:

### Tags:

#### *[Greedy algorithm](https://github.com/yang-233/Algorithm-note/tree/master/Greedy-algorithm)*

### How to do:

> Too simple. Due to the existence of 1. Must be able to find at least one combination. Just greedy to find a combination from big to small.We can use binary search to optimize the search.

### Code:

```c++
class Solution {
public:
    string getString(int num) {
        switch (num) {
            case 1:
                return "I";
            case 4:
                return "IV";
            case 5:
                return "V";
            case 9:
                return "IX";
            case 10:
                return "X";
            case 40:
                return "XL";
            case 50:
                return "L";
            case 90:
                return "XC";
            case 100:
                return "C";
            case 400:
                return "CD";
            case 500:
                return "D";
            case 900:
                return "CM";
            case 1000:
                return "M";
            default:
                return "";
        }
    }

    int binarySearch(const int a[], int val) {
        int l = 0, r = 12, ans = 0;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (a[mid] <= val) {
                ans = a[mid];
                l = mid + 1;
            } else
                r = mid - 1;
        }
        return ans;
    }

    string intToRoman(int num) {
        int a[] = {1, 4, 5, 9, 10, 40, 50, 90, 100, 400, 500, 900, 1000};
        vector<int> v;
        string ans;
        while (num) {
            v.push_back(binarySearch(a, num));
            num -= v.back();
        }
        for (int i:v)
            ans += getString(i);
        return ans;
    }

};
```

### Time complexity:

#### *O (?)*

### Space complexity:

#### *O(1)*

