# Reverse Linked List(LeetCode 206)  
## Description
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.   
__Example:__  
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
__Follow up:__  
Use a small heap to push each List's current head node. Use a new head to connect the dude poped from the small heap round by round. Easy.  
## Solution
__iterative:__
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* cur = nullptr;
        while (head!=nullptr) {
            ListNode* tmp = head -> next;
            head -> next = cur;
            cur = head;
            head = tmp;
        }
        return cur;
    }
};
```
__recursive：__
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head==nullptr||head->next==nullptr){
            return head;
        }
        ListNode* tmp=reverseList(head->next);
        head->next->next=head;
        head->next=nullptr;
        return tmp;
    }
};
```
[Reverse Linked List(LeetCode 206)](https://leetcode.com/problems/reverse-linked-list/) in LeetCode.