# Swap Nodes in Pairs(LeetCode 23)  
## Description
Given a linked list, swap every two adjacent nodes and return its head.
You may **not** modify the values in the list's nodes, only nodes itself may be changed.   
__Example:__  
```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```
## Solution
Use slow and fast pointer to follow. Be careful when the numbers of the nodes are odd.
A little stupid.
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
    ListNode* swapPairs(ListNode* head) {
        if(head==nullptr)return head;
        ListNode* dummy=new ListNode(0);
        ListNode* slow=head;
        ListNode* fast=head->next;
        if(fast==nullptr)return head;
        dummy->next=fast;
        while(fast!=nullptr){
            slow->next=fast->next;
            fast->next=slow;
            if(slow->next!=nullptr){
                if(slow->next->next==nullptr){
                    return dummy->next;
                }else{
                    fast=slow->next;
                    slow->next=slow->next->next;
                    slow=fast;
                    fast=fast->next;
                }
            }else{
                return dummy->next;
            }
        }
        return dummy->next;
    }
};
```
Or new a new list. Will use more space, but will cost less pointer manipilate.
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
    ListNode* swapPairs(ListNode* head) {
        if(head==nullptr)return head;
        ListNode* dummy=new ListNode(0);
        ListNode* slow=head;
        if(slow->next==nullptr)return slow;
        ListNode* fast=slow->next;
        ListNode* cur=dummy;
        while(1){
            cur->next=new ListNode(fast->val);
            cur=cur->next;
            cur->next=new ListNode(slow->val);
            cur=cur->next;
            if(fast->next!=nullptr){
                slow=fast->next;
                if(slow->next!=nullptr){
                    fast=slow->next;
                }else{
                    cur->next=new ListNode(slow->val);
                    break;
                }
            }else{
                break;
            }
        }
        return dummy->next;
    }
};
```
[Swap Nodes in Pairs(LeetCode 24)](https://leetcode.com/problems/swap-nodes-in-pairs/) in LeetCode.