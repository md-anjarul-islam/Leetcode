
```
class Solution {

public:
    int search(vector<int>& nums, int target) {
        int len = nums.size(), left = 0, right = len-1, mid = (left+right)/2;

        while(left<=right){
            mid = (left+right)/2;

            // if mid index is the target
            if(nums[mid] == target){
                return mid;
            }

            //is left half sorted? here equal condition checking is crucial
            // because if left and mid are equal then that is also sorted
            if(nums[left]<=nums[mid]){
                // if the target is in between them
                if(nums[left]<=target && target <= nums[mid]){
                    // previously we checked that nums[mid]==target?
                    // here we are sure that nums[mid]!=target
                    // so we can simply exclude the mid position from the search range
                    right = mid-1;
                }
                // target is not in the left half
                else{
                    left = mid+1;
                }
            }

            // if the right half is sorted
            else{
                // if the target is in between them
                if(nums[mid]<=target && target <= nums[right]){
                    // previously we checked that nums[mid]==target?
                    // here we are sure that nums[mid]!=target
                    // so we can simply exclude the mid position from the search range
                    left = mid+1;
                }
                // target is not in the left half
                else{
                    right = mid-1;
                }
            }
        }

        return -1;
    }
};
```
