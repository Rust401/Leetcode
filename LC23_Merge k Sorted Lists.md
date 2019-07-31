# Merge k Sorted Lists(LeetCode 23)  
## Description
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity. 
__Example 1:__  
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```
## Solution
Use a small heap to push each List's current head node. Use a new head to connect the dude poped from the small heap round by round. Easy.
```cpp
/*
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
struct cmp 
{
    bool operator () (ListNode *a, ListNode *b) 
    {
        return a->val > b->val;
    }
};

class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) 
    {
        priority_queue<ListNode*,vector<ListNode*>,cmp> smallHeap;
        for(int i=0;i<lists.size();++i)if(lists[i])smallHeap.push(lists[i]);
        ListNode* dummy=new ListNode(0);
        ListNode* cur=dummy;
        while(!smallHeap.empty())
        {
            cur->next=smallHeap.top();
            smallHeap.pop();
            cur=cur->next;
            if(cur->next)smallHeap.push(cur->next);
        }
        return dummy->next;
    }
};
```
[Merge k Sorted Lists(LeetCode 23)](https://leetcode.com/problems/merge-k-sorted-lists/) in LeetCode.