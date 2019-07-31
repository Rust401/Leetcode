# Remove Nth Node From End of List(LeetCode 19)  
## Description
Given a linked list, remove the n-th node from the end of list and return its head.  
__Example:__  
```txt
Given linked list: 1->2->3->4->5, and n = 2.
After removing the second node from the end, the linked list becomes 1->2->3->5.
```
__Note:__  
Given n will always be valid.
## Solution
* Basic two-pointer, use dummy to handle the edge situation.
```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(head==nullptr||n<1)return nullptr;
        ListNode* dummy=new ListNode(0);
        dummy->next=head;
        ListNode* slow=dummy;
        ListNode* fast=dummy;
        while(n--){
            fast=fast->next;
        }
        while(fast&&fast->next){
            fast=fast->next;
            slow=slow->next;
        }
        slow->next=slow->next->next;
        return dummy->next;
    }
};
```
[Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) in LeetCode.