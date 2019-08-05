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
__iterative:__
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

[Reverse Linked List II(LeetCode 92)](https://leetcode.com/problems/reverse-linked-list-ii/) in LeetCode.