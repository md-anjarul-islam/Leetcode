# Solution 1
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());

        vector<vector<int>> result;
        int len = intervals.size();
        int i = 0, j;

        while(i<len){
            j = i;
            int currEnd = intervals[i][1];
            while(j<len && currEnd >= intervals[j][0]){
                currEnd = max(currEnd, intervals[j][1]);
                j++;
            }
            result.push_back({intervals[i][0], currEnd});
            i = j;
        }
        return result;
    }
};
```

# Solution 2
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        
        vector<vector<int>> result;

        sort(intervals.begin(), intervals.end());
        // lets initialize current interval
        vector<int> mergedInterval = intervals[0];
        int len = intervals.size();

        for(int i=0; i<len; i++){
            vector<int> interval = intervals[i];

            // if merged interval overlaps current interval
            if(mergedInterval[1] >= interval[0]){
                // merge them
                mergedInterval[1] = max(mergedInterval[1], interval[1]);
            }
            else {
                // push the merged interval to the result set
                // re-initialze mergedInterval to the current interval
                // why current interval? Because current interval is not
                // overlapping and thus not merged yet. so save it for next
                // iteration
                result.push_back(mergedInterval);
                mergedInterval = intervals[i];
            }
        }
        result.push_back(mergedInterval);

        return result;
    }
};
```
# Solution 3
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        
        sort(intervals.begin(), intervals.end());

        vector<vector<int>> result;
        int len = intervals.size();

        result.push_back(intervals[0]);
        int index = 0;

        for(int i=0; i<len; i++){
            // if results latest interval is overlapping.
            if(result[index][1]>=intervals[i][0]){
                result[index][1] = max(result[index][1], intervals[i][1]);
            }
            else{
                result.push_back(intervals[i]);
                index++; // update latest index;
            }
        }

        return result;
    }
};
```
