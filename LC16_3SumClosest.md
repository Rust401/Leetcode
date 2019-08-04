# 3Sum Closest(LeetCode 16)  
## Description
Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution. 
__Example:__  
```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
## Solution
Loop the first dude. Then use two-pointer to cover the remain two dudes.
```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        if(nums.size()<3)return 0;
        std::sort(nums.begin(),nums.end());
        int result=INT_MAX;
        int div=INT_MAX;
        for(int i=0;i<nums.size()-2;++i){
            if(nums[i]>=target&&target>=0){
                return nums[i]+nums[i+1]+nums[i+2];
            }
            int remain=target-nums[i];
            int l=i+1;
            int r=nums.size()-1;
            while(l<r){
                int newdiv=abs(nums[l]+nums[r]-remain);
                if(newdiv<div){
                    result=nums[i]+nums[l]+nums[r];
                    div=newdiv;
                }
                if(nums[l]+nums[r]<remain){
                    ++l;
                }else if(nums[l]+nums[r]>remain){
                    --r;
                }else{
                    return target;
                }
            }
        }
        return result;
    }
};
```
[3Sum Closest(LeetCode 16)](https://leetcode.com/problems/3sum-closest/) in LeetCode.