# LeetCode 25. Reverse Nodes in k-Group [link](https://leetcode.com/problems/reverse-nodes-in-k-group/)

## Problem description:

> Given a linked list, reverse the nodes of a linked list *k* at a time and return its modified list.
>
> *k* is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of *k* then left-out nodes in the end should remain as it is.
>
> **Note:**
>
> - Only constant extra memory is allowed.
> - You may not alter the values in the list's nodes, only nodes itself may be changed.

## Example:

```
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Inspired by *[this blog](https://blog.csdn.net/weiyongle1996/article/details/78473055)*.

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
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode *ans = new ListNode(-1), *root = ans;
        ans->next = head;
        int count = 0;
        for(auto i = head; i; i = i->next)
            ++count;
        while(count >= k) {
            for(int i = 1; i < k; ++i) {
                ListNode *temp = root->next;
                root->next = head->next;
                head->next = root->next->next;
                root->next->next = temp;
            }
            root = head;
            head = root->next;
            count -= k;
        }
        return ans->next;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

