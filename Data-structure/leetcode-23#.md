# LeetCode 23. Merge k Sorted Lists [link](https://leetcode.com/problems/merge-k-sorted-lists/)

## Problem description:

> Merge *k* sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

## Example:

```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## Solution:

### Tags:

### *[Data structure](https://github.com/yang-233/Algorithm-note/tree/master/Data-structure)* 

### How to do:

> Use quick sort.

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

    ListNode *mergeKLists(vector<ListNode *> &lists) {
        vector<int> v;
        ListNode head(0), *temp = &head;
        for (int i = 0; i < lists.size(); ++i) {
            while (lists[i]) {
                v.push_back(lists[i]->val);
                lists[i] = lists[i]->next;
            }
        }
        sort(v.begin(), v.end());
        for (auto i: v) {
            temp->next = new ListNode(i);
            temp = temp->next;
        }
        return head.next;
    }
};
```

### Time complexity:

#### *O (n\*log(n))*

### Space complexity:

#### *O(n)*

