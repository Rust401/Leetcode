# Some Problems (3 min per problem)
## Description
some problems in the test of **ALIBABA**. No need to review before the test. Just use any method to solve it. 

## Problem List

1. There's a small town with 100 inhabits. One day a virus came in and make some people become wolves(At least one dude will become wolf). All the dwellers could only know others' appearance and they can't know whether their appearance has changed. And the dwellers can not talk to each other. If one dude know that he has been infected, he will leave the small town at the midnight.  **Now all the wolfves leave the town on the day 5 (the day begin at 0). How many wolves leave the town at day 3 and how many wolves in total?**


2. There is a complete binary tree in your garden with the deepth of 100. Each Node of the tree contains a flower. You could get your own specific bunch-of-flowers by tailing the the node from the tree. Now you want to get a bunch of flowers with the total flower number of **111100100111(binary)**. **What's the minium cutting times**?

3. Taylor expands to approach **1/e** with an error less than **10^-4**. **The orders of  Taylor expands we need?**

4. We have a server and it will be down at some time point. The down rate at **day_n** is depending on wether the server has been down at day **day_n-1** and day **day_n-2**. So if the server has been down at **day_0,day_1,day_2**. Please calculate the Downrate at **day_5**.

    ```txt
    if(isDown(n-1)&&isDown(n-2)){
        downRate=0.6
    }else if(isDown(n-1)||isDown(n-2)){
        downRate=0.4
    }else if(!isDown(n-1)&&!isDown(n-2)){
        downRate=0.1
    }
    ```

5. We have a wooden stick. We divide the stick into **4** parts randomly. Then we pick **3 of them** to try to build a triangle. Please calculate the rate that the we could use this 3 sub-sticks to build a triangle.

6. A string is **"aAbBcCdDeEfFgGhHiIjJkKlLmMnN"**. We could only swap adjacent characters. If we want to use swap to change the string to **"abcdefghijklmnABCDEFGHIJKLMN"**. How many times should we swap **at least**?

7. We have 64 bits all have the value 0. Each bit has an index start from **0** and end with **63**. Now we generate 64 random numbers range from 0 to 63. The bit with the index equal to the generated random number will become 1. So after 64 generating the rate of the 1 in the 64 bits will be?
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