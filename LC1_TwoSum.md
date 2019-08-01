# Two Sum(LeetCode 1)  
## Description
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.
###example
```txt
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## Solution
_the orginal one_
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        vector<int> sum;
        for(int i=0;i<nums.size()-1;i++)
        {
            for(int j=i+1;j<nums.size();j++)
            {
                if(nums[i]+nums[j]==target)
                {
                    sum.push_back(i);
                    sum.push_back(j);
                    return sum;
                }
            }
        }
        return sum;
    }
};
```
_the better one_
```cpp
class Solution {
public:
    vector<int> twoSum(std::vector<int>& nums, int target) {
        vector<int> res(2);
        unordered_map<int, int> test;
        for(int i = 0; i < nums.size(); ++i){
            auto it = test.find(target - nums[i]);
            if(it != test.end()){
                res[0] = it->second;
                res[1] = i;
                return res;
            } else	test.emplace(nums[i], i);
        }
        return res;
    }
};
```
[Two Sum(LeetCode 1)](https://leetcode.com/problems/two-sum) in LeetCode.