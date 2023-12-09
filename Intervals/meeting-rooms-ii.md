# Solution 1:
```cpp
/**
    Observations:
        - The meeting that starts earliest should be processed earlier
        - All the meetings coming up within that meeting time must 
         need a separate room
        - But there's a hack. Some meeting can be longer. But in the 
         mean time some other shorter meetings could take place. And
         those shorter meeting (if not overlapped) can be taken in
         using some rooms. Total Room won't be equal to the number of
         short meetings in the longer meeting interval. Because some
         short meetings will be finished earlier
        - if a meeting ends up we will clear that room and will reuse
         for the new meeting

    Solution:
        - We can keep a priority_queue to maintain the rooms.
        - If a meeting starts and there is no room we will add
          that meeting to a new room
        - If a meeting ends up we will remove that meeting
        - The maximum number of rooms at any moment is the 
          answer
*/
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());

        priority_queue<int, vector<int>, greater<int>> pq;
        int ans = 1;

        for(auto &interval: intervals){
            // all the intervals that were ended up should be removed
            while(pq.size() && pq.top() <= interval[0] ){
                pq.pop();
            }

            // add new meeting to the room
            pq.push(interval[1]);
            // check the current number of rooms
            ans = max(ans, (int)pq.size());
        }
        return ans;
    }
};
```
# Solution 2:
```cpp
/**
    Idea:
        - It is easily understandable that the problem asks for the
         number of rooms required for the most overlapping meeting
         time.
        - So, how can we calculate the max overlap count?
        - See the interval range is not that high
        - We can keep cumulative count to calculate the answer
*/
#define MAX_END 1000000

class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        int maxinterval = 0;
        vector<int> overlaps(MAX_END+2, 0);

        // increment for starting position
        // decrement for ending position
        for(auto &interval: intervals){
            overlaps[interval[0]]++;
            overlaps[interval[1]]--;
            maxinterval = max(maxinterval, interval[1]);
        }

        int ans = 0;

        // cumulatively sum up and get the answer
        for(int i=1; i<=maxinterval; i++){
            overlaps[i] += overlaps[i-1];
            ans = max(ans, overlaps[i]);
        }

        return ans;
    }
};
```
