# LeetCode 4. Median of Two Sorted Arrays [link](https://leetcode.com/problems/median-of-two-sorted-arrays/)

## Problem description:

> There are two sorted arrays **nums1** and **nums2** of size m and n respectively.
>
> Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
>
> You may assume **nums1** and **nums2** cannot be both empty.

## Example:

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## Solution:

### Tags:

#### *[Search](https://github.com/yang-233/Algorithm-note/tree/master/Search)* 

### How to do:

> According the definition of the median, we can convert the problem to be a problem that how to find *the kth number* in two sorted arrays. 
>
> For convenience, we define *i* and *j* to be the arrays' beginning. We consider three simple situations first:
>
> 1 *if i >= n* , means that the values in *nums1* have been invalid. Thus, *nums1*  is equivalent to an empty array.
>
> 2 if *j >= m*, the situation is similar with 1.
>
> 3 if *k == 1*, the *kth number* is *min(nums1[i], nums2[j])*.
>
> Now, let's deal with the general situation:
>
> We must reduce of the search range. How to do this? We just need to modify *i, j, k*.  Now, we want to reduce the range from *k* to *k/2*. We define *midVal1 = nums1[i + k / 2 - 1]*(if the *i +k / 2 - 1* >= n, the *midVal1 = INT_MAX*). The same reason, *midVal2* has the same definition in *nums2*. (Because the *k* must less than or equal to *(n + m)*, at least of  *midVal1* and *midVal2* is valid rather than *INT_MAX*.) And, we will find that if *midVal1 < midVal2* the *(k - k / 2)th number* can not appear in *nums1[i, i + k / 2 -1]*, if the situation is reversed, the *(k - k / 2)th number* can not appear in *nums2[j, j + k / 2 -1]*.
>
> Inspired by [this article](http://www.cnblogs.com/grandyang/p/4465932.html).

### Code:

```c++
class Solution {
public:
    int n, m;

    int findKth(vector<int> &nums1, int i, vector<int> &nums2, int j, int k) {
        if (i >= n)//the kth number can not appear in nums1
            return nums2[j + k - 1];
        if (j >= m)//the kth number can not appear in nums2
            return nums1[i + k - 1];
        if (k == 1)
            return min(nums1[i], nums2[j]);
        int mk = k / 2;
        int midVal1 = ((i + mk - 1) < n) ? nums1[i + mk - 1] : INT_MAX;
        int midVal2 = ((j + mk - 1) < m) ? nums2[j + mk - 1] : INT_MAX;
        //the (k - k/2)th number can not appear in nums1[i, i + mk - 1]. 
        if (midVal1 < midVal2)
            return findKth(nums1, i + mk, nums2, j, k - mk);
        else//the (k - k/2)th number can not appear in nums2[j, j + mk - 1].
            return findKth(nums1, i, nums2, j + mk, k - mk);
    }

    double findMedianSortedArrays(vector<int> &nums1, vector<int> &nums2) {
        n = nums1.size();
        m = nums2.size();
        if ((n + m) & 1)
            return findKth(nums1, 0, nums2, 0, (n + m + 1) / 2);
        else
            return (findKth(nums1, 0, nums2, 0, (n + m + 1) / 2) 
                    + findKth(nums1, 0, nums2, 0, (n + m + 2) / 2)) / 2.0;
    }
};
```

### Time complexity:

#### *O(log(m+n))*

### Space complexity:

#### *O(n)*

