# Reverse Linked List(LeetCode 206)  
## Description
Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.
__Example:__  
```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```
## Solution
Fvking easy. Just reverse.
__1:__
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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        ListNode* dummy=new ListNode(-1);
        ListNode* pre=dummy;
        pre->next=head;
        for(int i=1;i<m;i++){
            pre=pre->next;
        }
        head=pre->next;
        for(int i=1;i<=n-m;i++){
            ListNode *tmp=pre->next;
            pre->next=head->next;
            head->next=head->next->next;
            pre->next->next=tmp;
        }
        return dummy->next;
    }
};
```
__2:__
```cpp
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        if(head==nullptr||head->next==nullptr){
            return head;
        }
        int mm=m;
        int pm=m-1;
        int nn=n;
        ListNode* dummy=new ListNode(0);
        dummy->next=head;
        ListNode* slow=dummy;;
        ListNode* fast=dummy;
        ListNode* pre=dummy;
        while(pm--){
            pre=pre->next;
            slow=slow->next;
        }
        slow=slow->next;
        while(nn--){
            fast=fast->next;
        }
        fast=fast->next;
        int times=n-m+1;
        while(times--){
            ListNode* tmp=slow->next;
            slow->next=fast;
            fast=slow;
            slow=tmp;
        }
        pre->next=fast;
        ListNode* result=dummy->next;
        delete dummy;
        return result;
    }
};
```

[Reverse Linked List II(LeetCode 92)](https://leetcode.com/problems/reverse-linked-list-ii/) in LeetCode.