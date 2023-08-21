# Problem
Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2).

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).


# Solution
```
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        priority_queue<pair<int, int>> pq;

        int len = points.size();

        for(int i=0; i<len; i++){
            vector<int> point = points[i];
            int distance = point[0]*point[0] + point[1]*point[1];

            pq.push({distance, i});
            if(pq.size()>k){
                pq.pop();
            }
        }

        vector<vector<int>> ans;

        while(!pq.empty()){
            pair<int, int> top = pq.top();
            ans.push_back(points[top.second]);
            pq.pop();
        }

        return ans;
    }
};
```
