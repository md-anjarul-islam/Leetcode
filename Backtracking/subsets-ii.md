```cpp
/*
    Brute force combination generator
*/
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        int i=0, len = nums.size();
        int N = (1<<len);
        set<vector<int>>ans;

        for(int i=0; i<N; i++){
            vector<int> seq;
            for(int j=0; j<len; j++){
                if(i&(1<<j)) {
                    seq.push_back(nums[j]);
                }
            }
            sort(seq.begin(), seq.end());
            ans.insert(seq);
        }

        return vector<vector<int>> (ans.begin(), ans.end());
    }
};
```
