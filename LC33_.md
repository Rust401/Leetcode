# Remove Duplicates from Sorted Array(LeetCode 26)  
## Description
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
__Example1:__  
```txt
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

__Example2:__  
```txt
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```
__Clarification:__  
Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.

Internally you can think of this:
```txt
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
## Solution
Easy 2-pointer problem
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=1){
            return nums.size();
        }
        int slow=0;
        int fast=1;
        int count=1;
        while(fast<nums.size()){
            if(nums[fast]==nums[fast-1]){
                ++fast;
                continue;
            }
            nums[++slow]=nums[fast++];
            ++count;
        }
        return count;         
    }
};
```
A more delicated solution to be figure out.
[Remove Duplicates from Sorted Array(LeetCode 26)](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) in LeetCode.