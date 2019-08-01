# Container With Most Water(LeetCode 11)  
## Description
GGiven n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
Note: You may not slant the container and n is at least 2.

## Solution
_the orginal one_
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxVol=0,tempVol=0,h=0;
        for(int i=0;i<height.size()-1;i++){
            for(int j=i+1;j<height.size();j++){
                if(height[i]<height[j])
                    h=height[i];
                else    
                    h=height[j];
                tempVol=(j-i)*h;
                if(tempVol>maxVol)
                    maxVol=tempVol;
            }
        }
        return maxVol;
    }
};
```
_the better one_
```cpp
class Solution {
public:
    int maxArea( vector<int>& height ) {
        int maxVol = -1;
        int start = 0;
        int end = height.size() - 1;
        int temp;
        while( start < end ) {
            temp = min( height[start], height[end] ) * ( end-start );
            if( maxVol < temp  ) maxVol = temp;
            if( height[start] < height[end] )
                start++;
            else
                end--;
        }
        return maxVol;
    }
};
```

[Container With Most Water(LeetCode 11)](https://leetcode.com/problems/container-with-most-water/) in LeetCode.