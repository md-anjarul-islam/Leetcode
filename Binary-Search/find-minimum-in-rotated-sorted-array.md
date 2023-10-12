    
    Observation: If an array is sorted and has only unique numbers, then without
    rotation the arr[leftmost] < arr[midpos] < arr[rightmost] will be true.

    But what if we rotate the array?
    Let's think an example

    Rotation   ||         Array          ||    Condition       || Result (Side)
    ------------------------------------------------------------------------------
    0-rotation || arr: [1, 2, 3, 4, 5]   ||  arr[m] < arr[r]   || Left
    1-rotation || arr: [5, 1, 2, 3, 4]   ||  arr[m] < arr[r]   || Left
    2-rotation || arr: [4, 5, 1, 2, 3]   ||  arr[m] < arr[r]   || Left
    3-rotation || arr: [3, 4, 5, 1, 2]   ||  arr[m] > arr[r]   || Right
    4-rotation || arr: [2, 3, 4, 5, 1]   ||  arr[m] > arr[r]   || Right


    class Solution {
    public:
      int findMin(vector<int>& nums) {
          int left=0, right = nums.size()-1, mid;
  
          int ans = INT_MAX;
  
          while(left<=right){
              mid = (left+right)/2;
  
              // if left half is sorted
              if(nums[left] <= nums[mid]){
                  // and the left half's max number is greater than the right
                  if(nums[mid] > nums[right]){
                      left = mid+1;
                  }
                  else{
                      right = mid-1;
                  }
              }
              
              // else only right half is sorted
              // rotated part came to the left side.
              // so the minimum one is also there
              else {
                  right = mid-1;
              }
  
              ans = min(ans, nums[mid]);
          }
  
          return ans;
      }
      };
