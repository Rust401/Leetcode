# Two Sum(LeetCode 1)  
## Description
Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the same element twice.   
__Example:__  
```txt
    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].
```
## Solution
Use hashMap to record. If the **target-nums[i]** of new dude is the same to some dude in the map. We could directly return the result. Or we should insert the new dude.  
O(n) time.
O(n) space.
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::vector<int> result;
        if(nums.size()==0)return result;
        unordered_map<int,int> hashMap;
        for(int i=0;i<nums.size();++i){
            if(hashMap.count(target-nums[i])){
                return {hashMap[target-nums[i]],i};
            }else{
                hashMap.insert({nums[i],i});
            }
        }
        return result;
    }
};
```
[Two Sum](https://leetcode.com/problems/two-sum/)in leetcode.