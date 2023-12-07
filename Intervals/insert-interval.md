```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> result;

        for(auto &interval:intervals){
            // not overlapping and even not reached yet
            if(interval[1]<newInterval[0]){
                result.push_back(interval);
            }
            // just passing or already passed overlapping
            else if(interval[0] > newInterval[1]){
                // when we are just passing (first interval that is not overlapping)
                // we need to push the newInterval here
                result.push_back(newInterval);
                // and then there's two way. Either I can loop trough the
                // end and take all of them to the result array and return.
                // or to keep things clean we can move forward the current interval by using newInterval variable
                newInterval = interval;
            }
            // overlapped
            else {
                newInterval[0] = min(newInterval[0], interval[0]);
                newInterval[1] = max(newInterval[1], interval[1]);
            }
        }

        // finally push the newInterval.
        // it can have the original new interval (when the new interval is higher than all the intervals)
        // or it can have the 'forwarded interval'.
        result.push_back(newInterval);

        return result;
    }
};
```
