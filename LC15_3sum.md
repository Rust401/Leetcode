# 3Sum(LeetCode 15)  
## Description
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.   
__Note:__  
```txt
    The solution set must not contain duplicate triplets.
```  
__Example:__  
```txt
    Given array nums = [-1, 0, 1, 2, -1, -4],
    A solution set is:
    [
    [-1, 0, 1],
    [-1, -1, 2]
    ]
```
## Solution
Sort the array at first. Cost O(nlog(n)). Then we use a loop to follow the minum dude in the tripple. Kick off the impossible situation, such as the first dude is negative. Use to pointer to decide the remain two dude.
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        if(nums.size()<3)return {};
        std::vector<std::vector<int>> result;
        std::sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size()-2;++i){
            if(nums[i]>0)break;
            if(i>0&&nums[i]==nums[i-1])continue;
            int l=i+1;
            int r=nums.size()-1;
            int target=0-nums[i];
            while(l<r){
                if(nums[l]+nums[r]<target){
                    ++l;
                }else if(nums[l]+nums[r]>target){
                    --r;
                }else{
                    result.push_back({nums[i],nums[l],nums[r]});
                    while(l<r&&nums[l]==nums[l+1]){
                        ++l;
                    }
                    while(l<r&&nums[r]==nums[r-1]){
                        --r;
                    }
                    ++l;
                    --r;
                }
            }
        }
        return result;
    }
};
```
[3Sum(LeetCode 15)](https://leetcode.com/problems/3sum/) in LeetCode.