# Problem
Given an integer array nums of unique elements, return all possible 
subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

# Solution 1
```
class Solution {
    int N;
    vector<vector<int>> ans;
    vector<int> seq;

    void backtrack(int pos, vector<int> &nums){
        if(pos == N){
            ans.push_back(seq);
            return;
        }

        // take this number
        seq.push_back(nums[pos]);
        backtrack(pos+1, nums);
        
        // skip this number
        seq.pop_back();
        backtrack(pos+1, nums);
    }
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        N = nums.size();

        backtrack(0, nums);

        return ans;
    }
};

```
# Solution 2
```
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int i=0, len = nums.size();
        int N = (1<<len);
        vector<vector<int>>ans;

        for(int i=0; i<N; i++){
            vector<int> seq;
            for(int j=0; j<len; j++){
                if(i&(1<<j)) {
                    seq.push_back(nums[j]);
                }
            }
            ans.push_back(seq);
        }

        return ans;
    }
};
```
