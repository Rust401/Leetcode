# Next Permutation(LeetCode 31)  
## Description
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

###example
```txt
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```
## Solution
```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int len=nums.size();
        int trans;
        int pivot;
        if(len<=1) return;
        if(len==2){
            swap(nums[0],nums[1]);
            return;
        }
        for(int i=len-1;i>0;i--){
            if(nums[i]>nums[i-1]){
                if(i==len-1){
                    swap(nums[i],nums[i-1]);
                    return;
                }
                trans=i-1;//0
                pivot=i;
                for(int j=i;j<len;j++){
                    if(nums[j]>nums[trans]&&nums[j]<nums[pivot]){
                        pivot=j;
                    }
                }
                swap(nums[pivot],nums[trans]);
                sort(nums.begin()+i,nums.end());
                return;
            }
        }
        sort(nums.begin(),nums.end());
    }
};
```

[Next Permutation(LeetCode 31)](https://leetcode.com/problems/next-permutation/) in LeetCode.