```cpp
/*
  Try all candidates recursively.
  - Take a number
  - Subtract the value from target
  - Recursively solve for the new target
  - To re-use a value start looping from already previously taken value
*/

class Solution {
    vector<vector<int>> ans;

    void solve(vector<int>& candidates, int target, vector<int>& selected, int start_from){

        // if target is filled-up then take the selected into result
        if(target == 0){
            ans.push_back(selected);
            return;
        }
        
        int len = candidates.size();

        // try all candidates.
        // but skip previously taken candidates to avoid duplication
        for(int i = start_from; i<len; i++){
            // if current candidate can be taken
            // then take it and subtract the value from target
            int cand = candidates[i];
            if(cand<=target){
                selected.push_back(cand);
                // subtract from target
                solve(candidates, target-cand, selected, i);
                // remove from selected list for next recursion
                selected.pop_back();
            }
        }
    }
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> selected;

        solve(candidates, target, selected, 0);

        return ans;
    }
};
```
