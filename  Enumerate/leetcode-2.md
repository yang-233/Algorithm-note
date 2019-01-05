# LeetCode 2. Add Two Numbers [link](https://leetcode.com/problems/add-two-numbers/)

## Problem description:

> You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Example:

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## Solution:

### Tag:

#### *[ Enumerate](https://github.com/yang-233/Algorithm-note/tree/master/Search)* 

### How to do:

> You can do it according to the definition of addition.

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *ans=NULL;
        ListNode **t=&ans;
        int last=0,res=0;
        while(l1&&l2){
            res=l1->val+l2->val+last;
            last=res/10;
            *t=new ListNode(res%10);
            t=&(*t)->next;
            l1=l1->next;
            l2=l2->next;
        }
        while(l1){//l1.size>l2.size
            res=l1->val+last;
            last=res/10;
            *t=new ListNode(res%10);
            t=&(*t)->next;
            l1=l1->next;
        }
        while(l2){//l1.size<l2.size
            res=l2->val+last;
            last=res/10;
            *t=new ListNode(res%10);
            t=&(*t)->next;
            l2=l2->next;
        }
        if(last){
            *t=new ListNode(last);
        }
        return ans;
    }
};
```

### Time complexity:

#### *O(n)*

### Memory complexity:

#### *O(n)*

