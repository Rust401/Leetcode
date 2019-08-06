# Partition List(LeetCode 86)  
## Description
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.
__Example:__  
```
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```
## Solution
__1:__
Recursion, waste memory and have repeat walk through.
```cpp
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        if(head==nullptr||head->next==nullptr){
            return head;
        }
        ListNode* dummy=new ListNode(0);
        dummy->next=head;
        ListNode* pre=dummy;
        ListNode* after;
        ListNode* bigHead=head;
        ListNode* bigTail;
        ListNode* smallHead;
        ListNode* smallTail;
        while(bigHead!=nullptr&&bigHead->val<x){
            bigHead=bigHead->next;
            pre=pre->next;
        }
        if(bigHead==nullptr){
            return dummy->next;
        }
        smallHead=bigHead;
        bigTail=pre;
        while(smallHead!=nullptr&&smallHead->val>=x){
            smallHead=smallHead->next;
            bigTail=bigTail->next;
        }
        if(smallHead==nullptr){
            return dummy->next;
        }
        smallTail=bigTail;
        after=smallHead;
        while(after!=nullptr&&after->val<x){
            after=after->next;
            smallTail=smallTail->next;
        }
        pre->next=smallHead;
        bigTail->next=after;
        smallTail->next=partition(bigHead,x);
        return dummy->next;
    }
};
```
__2:__
Build two link-list and merge, easy to manupilate but cost memory
```cpp
class Solution {
public:
    ListNode* partition(ListNode* head, int x) 
    {
        ListNode* smallHead=new ListNode(0);
        ListNode* bigHead=new ListNode(0);
        ListNode* curSmall=smallHead;
        ListNode* curBig=bigHead;
        ListNode* cur=head;
        while(cur)
        {
            ListNode* tmp=new ListNode(cur->val);
            if(tmp->val>=x)
            {
                curBig->next=tmp;
                curBig=curBig->next;
            }
            else
            {
                curSmall->next=tmp;
                curSmall=curSmall->next;
            }
            cur=cur->next;
        }
        curSmall->next=bigHead->next;
        return smallHead->next;
    }
};
```
__3:__
The iteration version of method 1, ugly!! But fast.
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
    ListNode* partition(ListNode* head, int x) {
        if(head==nullptr||head->next==nullptr){
            return head;
        }
        ListNode* dummy=new ListNode(0);
        dummy->next=head;
        ListNode* pre=dummy;
        ListNode* after;
        ListNode* bigHead=head;
        ListNode* bigTail;
        ListNode* smallHead;
        ListNode* smallTail;
        while(bigHead!=nullptr&&bigHead->val<x){
            bigHead=bigHead->next;
            pre=pre->next;
        }
        if(bigHead==nullptr){
            return dummy->next;
        }
        smallHead=bigHead;
        bigTail=pre;
        while(smallHead!=nullptr&&smallHead->val>=x){
            smallHead=smallHead->next;
            bigTail=bigTail->next;
        }
        if(smallHead==nullptr){
            return dummy->next;
        }
        smallTail=bigTail;
        after=smallHead;
        while(after!=nullptr&&after->val<x){
            after=after->next;
            smallTail=smallTail->next;
        }
        pre->next=smallHead;
        bigTail->next=after;
        smallTail->next=bigHead;
        while(after!=nullptr){
            pre=smallTail;
            while(bigTail->next!=nullptr&&bigTail->next->val>=x){
                bigTail=bigTail->next;
            }
            if(bigTail->next==nullptr){
                break;
            }
            smallHead=bigTail->next;
            smallTail=smallHead;
            while(smallTail->next!=nullptr&&smallTail->next->val<x){
                smallTail=smallTail->next;
            }
            after=smallTail->next;
            pre->next=smallHead;
            bigTail->next=after;
            smallTail->next=bigHead;    
        }
        return dummy->next;
    }
};
```

[Partition List(LeetCode 86)](https://leetcode.com/problems/partition-list/) in LeetCode.