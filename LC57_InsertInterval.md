# Insert Interval
## description
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.
__Example 1:__

        Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
        Output: [[1,5],[6,9]]
__Example 2:__

        Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
        Output: [[1,2],[3,10],[12,16]]
        Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
## Solution
Before we handle this problem, wo could solve the [Merge Interval(LeetCode56)](https://github.com/Rust401/Leetcode/blob/master/LC56_MergeInterval.md) first.  

        |__1__|  |___2___|  |__3__| |_4_|  |_5_|
                   |_____newInterval_____|

THe intervals are sorted. We could divide the intervals into 2 category. The dude who tange with the `newInterval`(e.g. 2,3,4) and the dude who is no connection with the `newInterval`(e.g 1,5).  
For the no-tanged dude, we just push them into the result vector. For the tanged dude, we should handle them with newInterval and combine them to a new BIG interval(maybe just the Interval itself). Here is the code:
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
class Solution {
public:
    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) 
    {
        vector<Interval> result;
        int n=intervals.size();
        //handle the special situation
        if(intervals.size()==0)
        {
            result.push_back(newInterval);
            return result;
        }
        //At the tail and no tanged
        if(newInterval.start>intervals.back().end)
        {
            result=intervals;
            result.push_back(newInterval);
            return result;
        }
        //At the head and no tanged
        if(newInterval.end<intervals[0].start)
        {
            result.push_back(newInterval);
            result.insert(result.end(),intervals.begin(),intervals.end());
            return result;
        }
        //core part
        int currentStart=newInterval.start;
        int currentEnd=newInterval.end;
        int flag=0;//use to mark if we enter the tanged part
        for(int i=0;i<n;++i)
        {
            if(intervals[i].end<newInterval.start||intervals[i].start>newInterval.end)//no tanged dude
            {
                if(intervals[i].end<newInterval.start&&intervals[i+1].start>newInterval.end)//No tanged but the newInterval is in the middle
                {
                    result.push_back(intervals[i]);
                    result.push_back(newInterval);
                }
                else//no tanged dude
                {
                    if(flag==1)//Finish the combined and push the combined dude to the result
                    {
                        result.push_back(Interval(currentStart,currentEnd));
                        flag=0;
                    }
                    result.push_back(intervals[i]); 
                }

            }
            else//Tanged and need combine
            {
                flag=1;//set the flag to 1 means we enter the 'combine section'
                currentStart=min(currentStart,intervals[i].start);
                currentEnd=max(newInterval.end,intervals[i].end);
                if(i==n-1)result.push_back(Interval(currentStart,currentEnd));//If reach the end of the intervals then push the combined dude into the result
            }
        }
        return result;
    }
};
```
There is another problem about interval [Merge Interval(LeetCode 56)](https://leetcode.com/problems/merge-intervals/) in LeetCode.