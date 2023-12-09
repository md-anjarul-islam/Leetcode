```cpp
/**
    Wrong Idea:
        - One may assume that we can always start with the smallest length
        of intervals because smalle length will always have less chance of
        overlapping. But that's wrong!!

        Considering this example
        [1, 10], [9, 12], [11, 20].

        See, if we start with smallest length interval then we are to
        take [9, 12] first. And then we can't take any others.

        But if we removed that smallest length interval then we could
        take the other two intervals.

    Correct Idea:
        - The correct Idea is, if we start processing with the earliest
        ending intervals then we will have more intervals to take.
        - So on first process, Among all of the intervals you must take 
        the interval that ends earlier. That's totally safe.
        - And now after taking that we know that upto that endings
        no other interval can be taken. We can now start finding the
        next interval that starts after that ending and also has the 
        earliest endings among the rest
*/

class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {

        //sort by ascending order of endings
        sort(intervals.begin(), intervals.end(), [](const auto &a, const auto &b){
            return a[1]<b[1];
        });

        // assume interval end
        int currentEnd = INT_MIN;
        int ans = 0;
        for(auto &interval: intervals){
            // if the current end has no overlapping with the current interval
            // then update the current end to the current interval end
            if(currentEnd <= interval[0]){
                currentEnd = interval[1];
            }
            // else current end overlaps. so need to remove
            else{
                ans++;
            }
        }

        return ans;
    }
};
```
