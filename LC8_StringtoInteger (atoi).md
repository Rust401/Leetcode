# String to Integer(LeetCode 8)  
## Description
Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

__Note:__
* Only the space character `' '` is considered as whitespace character.
* Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. If the numerical value is out of the range of representable values, INT_MAX (2^31 − 1) or INT_MIN (−2^31) is returned.

__Example 1:__  
```txt
    Input: "42"
    Output: 42
```
__Example 2:__
```txt
    Input: "   -42"
    Output: -42
    Explanation: The first non-whitespace character is '-', which is the minus sign.
                Then take as many numerical digits as possible, which gets 42.
``` 
__Example 3:__
```txt
    Input: "4193 with words"
    Output: 4193
    Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
``` 
__Example 4:__
```txt
    Input: "words and 987"
    Output: 0
    Explanation: The first non-whitespace character is 'w', which is not a numerical 
                digit or a +/- sign. Therefore no valid conversion could be performed.
``` 
__Example 5:__
```txt
    Input: "-91283472332"
    Output: -2147483648
    Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
                Thefore INT_MIN (−231) is returned.
``` 
## Solution
```cpp
class Solution {
public:
    int myAtoi(std::string& str){
        if(str.length()==0)return 0;
        str.erase(0,str.find_first_not_of(" "));
        if(str.length()==0)return 0;
        int flag=1;
        int64_t result=0;
        int cur=0;
        if(str[cur]=='+'){
            ++cur;
            if(cur<str.length()){
                if(str[cur]<'0'||str[cur]>'9')return 0;
            }else{
                return 0;
            }
        }
        if(str[cur]=='-'){
            ++cur;
            if(cur<str.length()){
                if(str[cur]<'0'||str[cur]>'9')return 0;
            }else{
                return 0;
            }
            flag=-1;
        }
        while(str[cur]>='0'&&str[cur]<='9'){
            result=result*10+(str[cur]-'0');
            ++cur;
            if(result>INT_MAX){
                if(flag==1){
                    return INT_MAX;
                }
                else{
                    return INT_MIN;
                }
            }
        }
        result=int(flag==1?result:-result);
        return result;
    }
};
```


[String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/) in LeetCode.