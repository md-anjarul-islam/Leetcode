```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        
        for(int num:nums){
            num = abs(num);
            // check mark
            if(nums[num] < 0) {
                return num;
            }
            // mark num's position
            nums[num]*=-1;
        }

        return -1;
    }
};
```
