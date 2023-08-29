# Problem
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

# Solution
```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> deq;
        vector<int> ans;
        int left = 0, right = 0, len = nums.size();

        while(right<k){
            while(deq.size() && nums[deq.back()] < nums[right]){
                deq.pop_back();
            }

            deq.push_back(right);
            right++;
        }

        ans.push_back(nums[deq.front()]);

        while(right<len){
            // as the queue size is now K. so remove the leftmost one and add right one
            // if the left pointer is the current max then we should delete that
            if(deq.front() == left){
                deq.pop_front();
            }
            // move the left pointer
            left++;
            // remove small numbers from the queue
            while(deq.size() && nums[deq.back()] <= nums[right]){
                deq.pop_back();
            }
            // add the right one
            deq.push_back(right);
            right++;
            // now take max from the latest queue
            ans.push_back(nums[deq.front()]);
        }

        return ans;
    }
};
```
