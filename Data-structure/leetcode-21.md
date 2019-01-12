# LeetCode 21. Merge Two Sorted Lists [link](https://leetcode.com/problems/merge-two-sorted-lists/)

## Problem description:

> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Example:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Create a pseudo-head node.

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode *_head = new ListNode(0), *t = _head;
        while(l1 && l2) {
            if(l1->val <= l2->val) {
                t->next = l1;
                t = t->next;
                l1 = l1->next;
            } else {
                t->next = l2;
                t = t->next;
                l2 = l2->next;
            }
        }
        if(l2)
            t->next = l2;
        if(l1)
            t->next = l1;
        return _head->next;
    }
};
```

### Time complexity:

#### *O (len)*

### Space complexity:

#### *O(1)*

