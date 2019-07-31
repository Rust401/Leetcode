# Merge Two Sorted Lists(LeetCode 21)  
## Description
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.  
__Example:__  
```txt
    Input: 1->2->4, 1->3->4
    Output: 1->1->2->3->4->4
```
## Solution
Remeber we want a new link list to return. So new the heap memory to connect the new node to a new head.
```cpp
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) 
    {
        ListNode* cur1=l1;
        ListNode* cur2=l2;
        ListNode* result=new ListNode(0);
        ListNode* cur3=result;
        while(cur1&&cur2)
        {
            int num1=cur1->val;
            int num2=cur2->val;
            if(num1>=num2)
            {
                cur3->next=new ListNode(num2);
                cur3=cur3->next;
                cur2=cur2->next;
            }
            else
            {
                cur3->next=new ListNode(num1);
                cur3=cur3->next;
                cur1=cur1->next;
            }
        }
        while(cur1)
        {
            cur3->next=new ListNode(cur1->val);
            cur3=cur3->next;
            cur1=cur1->next;
        }
        while(cur2)
        {
            cur3->next=new ListNode(cur2->val);
            cur3=cur3->next;
            cur2=cur2->next;
        }
        return result->next;
    }
};
```
[Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) in LeetCode.