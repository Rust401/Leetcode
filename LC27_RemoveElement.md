# Next Permutation(LeetCode 31)  
## Description
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

###example1
```txt
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```
###example2
```txt
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```
## Solution
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int pivot=nums.size()-1;
        int last=pivot;
        while(pivot>=0){
            if(nums[pivot]==val)
                swap(nums[pivot],nums[last--]);
            pivot--;
        }
        return last+1;
    }
};
```

[Remove Element(LeetCode 27)](https://leetcode.com/problems/remove-element/) in LeetCode.