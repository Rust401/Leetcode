# Longest Substring Without Repeating Characters(LeetCode 3)  
## Description
Given a collection of intervals,merge all overlapping intervals.  
__Example 1:__  
```txt
    Input: "abcabcbb"
    Output: 3 
    Explanation: The answer is "abc", with the length of 3. 
```
__Example 2:__
```txt
    Input: "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.
``` 
__Example 3:__
```txt
    Input: "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3. 
``` 
## Solution
* Use hash_set O(n)
```cpp
public:
    int lengthOfLongestSubstring(string s) {
        if(s.length()<=1)return s.length();
        int result=0;
        unordered_set<char> aSet;
        int slow=0;
        int fast=0;
        while(fast<s.length()){
            if(aSet.insert(s[fast]).second==false){
                aSet.erase(s[slow]);
                ++slow;
            }else{
                ++fast;
                result=max(result,fast-slow);
            }
        }
        return result;
    }
};
```
* Use hash_map O(n)
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) 
    {
        if(s.size()<2)return s.size();
        unordered_map<char,int> workingMap;
        int left=0;
        int result=0;
        for(int right=0;right<s.size();++right)
        {
            if(workingMap.count(s[right]))
            {
                left=max(workingMap[s[right]],left);
                workingMap[s[right]]=right+1;
            }
            else workingMap.insert({s[right],right+1});
            result=max(result,right-left+1);
        }
        return result;
    }
};
```
* Use ascii array O(n)
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) 
    {
        if(s.size()<2)return s.size();
        int index[128];
        memset(index,0,sizeof(index));
        int left=0;
        int result=0;
        for(int right=0;right<s.size();++right)
        {
            left=max(left,index[s[right]]);
            result=max(result,right-left+1);
            index[s[right]]=right+1;
        }
        return result;
    }
};
```


[Longest Substring Without Repeating Characters(LeetCode 3)](https://leetcode.com/problems/longest-substring-without-repeating-characters/) in LeetCode.