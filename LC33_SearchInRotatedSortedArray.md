# Search in Rotated Sorted Array(LeetCode 33)  
## Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).
__Example1:__  
```txt
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

__Example2:__  
```txt
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```
## Solution
Actually it's not that easy, cuz you should handle the boundary problem. Especially you face the situation such as the one of the pivot is built only by one numbers. Besides, the situation that the element in one of the pivot is same. So how to handle this is the key to get the solution. 
```cpp
class Solution {
public:
    int search(std::vector<int>& nums, int target) {
        if(nums.size()==0)return -1;
        if(nums.size()==1&&nums[0]!=target)return -1;
        if(nums.size()==1&&nums[0]==target)return 0;
        int l=0;
        int r=nums.size()-1;
        while(l<r){
            int mid=l+(r-l)/2;
            if(nums[mid]==target){
                return mid;
            }else if(nums[l]<=nums[mid]){
                if(target<=nums[mid]&&target>=nums[l]){
                    r=mid-1;
                }else{
                    l=mid+1;
                }
            }else{
                if(target>nums[mid]&&target<=nums[r]){
                    l=mid+1;
                }else{
                    r=mid-1;
                }
            }
        }
        if(nums[l]==target)return l;
        return -1;
    }
};
```
A more delicated solution to be figure out.
[Search in Rotated Sorted Array(LeetCode 33)](https://leetcode.com/problems/search-in-rotated-sorted-array/) in LeetCode.