# Reverse Nodes in k-Group(LeetCode 25)  
## Description
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.
__Example:__  
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
__Note:__
* Only constant extra memory is allowed.
* You may not alter the values in the list's nodes, only nodes itself may be changed.

## Solution
Use iteration and reverse link list. Fvking easy.
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
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(head==nullptr||head->next==nullptr){
            return head;
        }
        ListNode* cur=head;
        int count=0;
        while(cur!=nullptr&&count!=k){
            ++count;
            cur=cur->next;
        }
        if(count==k){
            cur=reverseKGroup(cur,k);
            while(k--){
                ListNode* tmp=head->next;
                head->next=cur;
                cur=head;
                head=tmp;
            }
            return cur;
        }
        return head;
    }
};
```

[Reverse Nodes in k-Group(LeetCode 25)](https://leetcode.com/problems/reverse-nodes-in-k-group/) in LeetCode.