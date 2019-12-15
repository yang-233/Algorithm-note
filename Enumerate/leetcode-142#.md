# [LeetCode 142. Linked List Cycle II](<https://leetcode.com/problems/linked-list-cycle-ii/>) 

## Problem description:

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

**Note:** Do not modify the linked list.

## Example:

>```
>Input: head = [3,2,0,-4], pos = 1
>Output: tail connects to node index 1
>Explanation: There is a cycle in the linked list, where tail connects to the second node.
>
>Input: head = [1,2], pos = 0
>Output: tail connects to node index 0
>Explanation: There is a cycle in the linked list, where tail connects to the first node.
>
>Input: head = [1], pos = -1
>Output: no cycle
>Explanation: There is no cycle in the linked list.
>```

## Solution:

### Tags:

#### *[Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Enumerate)* 

#### How to do:

> 画图可解。找出长度关系

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
    ListNode *detectCycle(ListNode *head) {
        auto slow = head, fast = head;
        while(fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if(fast == slow) {
                fast = head;
                while(fast != slow) {
                    fast = fast->next;
                    slow = slow->next;
                }
                return fast;
            }
        }
        return NULL;
    }
};
```

### Time complexity:

#### *O (n)*

### Space complexity:

#### *O(1)*

