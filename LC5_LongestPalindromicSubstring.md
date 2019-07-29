# Longest Palindromic Substring(LeetCode 5)  
## Description
Given a string `s`, find the longest palindromic substring in `s`. You may assume that the maximum length of s is 1000.
__Example 1:__  
```txt
    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.
```
__Example 2:__
```txt
    Input: "cbbd"
    Output: "bb"
``` 

## Solution
__DP__
```cpp
class Solution {
public:
    string longestPalindrome(const std::string& str) {
        if(str.length()<2)return str;
        std::vector<std::vector<bool>> dp(str.length(),std::vector<bool>(str.length(),false));
        std::string result="";
        int currentMax=0;
        for(int j=0;j<str.length();++j){
            for(int i=0;i<=j;++i){
                dp[i][j]=str[i]==str[j]&&(j-i<=2||dp[i+1][j-1]);
                if(dp[i][j]){
                    if(j-i+1>currentMax){
                        currentMax=j-i+1;
                        result=str.substr(i,j-i+1);
                    }
                }
            }
        }
        return result;
    }
};
```
__Expand__
```cpp
class Solution {
public:
    string result;
    string longestPalindrome(string s) 
    {
        if(s.length()==0)return result;
        for(int i=0;i<s.length();++i)
        {
            helper(s,i,i);
            helper(s,i,i+1);
        }
        return result;
    }
private:
    void helper(string s,int left,int right)
    {
        while(left>=0&&right<s.length()&&s[left]==s[right])
        {
            --left;
            ++right;
        }
        string cur=s.substr(left+1,right-left-1);
        if(cur.length()>result.length())result=cur;
    }
};
```

[Longest Palindromic Substring(LeetCode 5)](https://leetcode.com/problems/longest-palindromic-substring/) in LeetCode.