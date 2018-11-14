# Merge Interval(LeetCode 56)  
## Description
Given a collection of intervals,merge all overlapping intervals.  
__Example 1:__  

        Input: [[1,3],[2,6],[8,10],[15,18]
        Output: [[1,6],[8,10],[15,18]]
        Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
__Example 2:__

        Input: [[1,4],[4,5]]
        Output: [[1,5]]
        Explanation: Intervals [1,4] and [4,5] are considerred overlapping.
## Solution
Since the input `intervals` have no order. So we sort them at first. For each `Interval` in sorted `intervals`, if the one behind's `start` is smaller or equal to the current one's `end`, we combine them with the current one's `start` as the `newStart` and the bigger one of the `end` of  the two intervals as the `newEnd`. Now we get a new temporary Interval and continue our combining till the next interval's start is bigger than the `newEnd`. So let's see the code:

```cpp
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
bool compare(const Interval& I1,const Interval& I2)
{
    if(I1.start==I2.start)return I1.end<I2.end;
    return I1.start<I2.start;
}

class Solution 
{
public:
    vector<Interval> merge(vector<Interval>& intervals) 
    {
        vector<Interval> result;//The dude we will return
        //Handle the special situations
        if(intervals.size()==0)return result;
        else if(intervals.size()==1)
        {
            result.push_back(intervals[0]);
            return result;
        }
        //Sort the intervals with the compare function
        std::sort(intervals.begin(),intervals.end(),compare);
        
        //Record the first dude
        int currentStart=intervals[0].start;
        int currentEnd=intervals[0].end;

        for(int i=1;i<intervals.size();++i)
        {
            if(intervals[i].start<=currentEnd)//Need combine
            {
                currentEnd=max(intervals[i].end,currentEnd);//Update the currentEnd after combined.
                //If this is the last interval we just push it to the result
                if(i==intervals.size()-1)result.push_back(Interval(currentStart,currentEnd));
            }
            else//No need to combine
            {
                //This is the last dude. Push the last combined dude and push the last dude
                if(i==intervals.size()-1)
                {
                    result.push_back(Interval(currentStart,currentEnd));
                    result.push_back(intervals[i]);
                }
                else//Push the former combined one and update the newStart and newEnd
                {
                    result.push_back(Interval(currentStart,currentEnd));
                    currentStart=intervals[i].start;
                    currentEnd=intervals[i].end;
                }
            }
        }
        return result;   
    }    
};
```
There is another problem about interval [Insert Interval(LeetCode 57)](https://leetcode.com/problems/insert-interval/) in LeetCode.
