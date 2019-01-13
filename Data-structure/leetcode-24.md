# LeetCode 24. Swap Nodes in Pairs [link](https://leetcode.com/problems/swap-nodes-in-pairs/)

## Problem description:

> Given a linked list, swap every two adjacent nodes and return its head.
>
> **Note:**
>
> - Your algorithm should use only constant extra space.
> - You may **not** modify the values in the list's nodes, only nodes itself may be changed.

## Example:

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Note handling null pointers.

### Code:

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *swapPairs(ListNode *head) {
        if(!head)
            return NULL;
        for (ListNode *i = head, *j = i->next;;) {
            if (!i || !j)
                break;
            swap(i->val, j->val);
            i = j->next;
            if (i)
                j = i->next;
            else
                break;
        }
        return head;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

