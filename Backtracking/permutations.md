```cpp
/*
  Backtracking:
    - Take a number
    - Mark as taken
    - Recursively move forward until all the numbers are taken
    - Remove mark to consider on another recursion
*/

class Solution {
    vector<vector<int>> ans;
    vector<bool> isTaken;
    vector<int> perm;

    void solve(vector<int> &nums){
        // when all numbers are taken then take the answer and return
        if(perm.size() == nums.size()){
            ans.push_back(perm);
            return;
        }

        for(int i=0; i<nums.size(); i++){
            if(isTaken[i] == false){
                // if not taken yet then take it
                perm.push_back(nums[i]);
                isTaken[i] = true;
                // recursively move forward
                solve(nums);

                // remove taken for the next recursion
                perm.pop_back();
                isTaken[i] = false;
            }
        }
    }
public:
    vector<vector<int>> permute(vector<int>& nums) {
        isTaken = vector<bool> (6, false);

        solve(nums);

        return ans;
    }
};
```
