```cpp
/**
    nums: [2,3,1,1,4]
    index:[0,1,2,3,4]

    jump from 0 => 1, 2
    jump from 1 => 2, 3, 4
    jump from 2 => 3
    jump from 3 => 4
    jump from 4 => 5, 6, 7, 8


    Here some points to consider
    1. From any i'th index we can reach to any index in range [i, i+nums[i]]
    2. But let's say nums[i+nums[i]] = 0. That means we can't jump from the end of the current range
    3. So we may need to jump from it's previous index.
    4. From where we will jump? We will jump from such index so that we can reach farthest index
    5. How do we know the farthest reachable index?
    6. Calculate the max reachable index at all the indexes
    7. Take the maximum of them always. (That will be the max reachable index)
    8. Now if we got stuck at any index where we reached the end of the current range but cant jump farther then consider jumping from a previous index
    9. So greedily take the max reachable index from previous jump
    10. Increment total jump count
*/

class Solution {
public:
    int jump(vector<int>& nums) {
        
        int currentMaxReach = 0, currentMaxPossible=0;
        int totalJump = 0;

        int len = nums.size();
        for(int i=0; i<len-1; i++){
            currentMaxPossible = max(currentMaxPossible, i+nums[i]);

            if(currentMaxReach == i){
                currentMaxReach = currentMaxPossible;
                totalJump++;
            }
        }

        return totalJump;
    }
};
```
