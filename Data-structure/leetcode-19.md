# LeetCode 19. Remove Nth Node From End of List [link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

## Problem description:

> Given a linked list, remove the *n*-th node from the end of list and return its head.
>
> **Note:**
>
> Given *n* will always be valid.
>
> **Follow up:**
>
> Could you do this in one pass?

## Example:

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Use the two pointer approach. Create a pseudo-head node to delete the head node.

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

    ListNode *removeNthFromEnd(ListNode *head, int n) {
        ListNode *fast, *slow;
        ListNode _head(-1);
        _head.next = head;
        fast = slow = &_head;
        for (int i = 0; i <= n; i++)
            fast = fast->next;
        while (fast) {
            slow = slow->next;
            fast = fast->next;
        }
        ListNode *tmep = slow->next;
        slow->next = slow->next->next;
        delete temp;
        return _head.next;
    }
};
```

### Time complexity:

#### *O (len)*

### Space complexity:

#### *O(1)*

