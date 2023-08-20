/**
    Given: 2,1,5,6,2,3
    Let's iterate over the array and consider each element to be
    a possible candidate height for the final result.

    Take the first height 2:
        To get the max possible area for height 2 we need to know
        the subarray to the left & right from 2 where 2 will be smallest
        among them.
        Till now we don't know how far we can get to the right so that 2
        remains smallest. So we don't know the result of 2 yet as well.
        Let's pause it's calculation for future. (maintain a pause list)

    Go to the next height 1:
        Again we don't how far we can get to the right so that 1
        remains smallest.

        But earlier we paused calculation for 2 because we didn't know the
        upper bound for that. But now as we've got a smaller number "1"
        so 2 is no more the smallest. Right?
        It clearly appears that, this is the upper bound of 2. Right?

        Though we've got the upper bound of 2, what is the lower bound?

        Before answering the question, let's look into some other observations.

        Do we need to keep 2 in the paused list anymore?
        
        No. Because as we've got the upper bound of 2 we don't need to 
        extend it anymore. We can calculate result for 2 here and remove 
        it from the paused list.

        So basically when we are getting a new height, we can remove all
        the bigger heights from the paused list. Because we don't need them
        anymonre.

        Thus the paused list will always be sorted in increasing order.
        Right?
   
        Here's the simulation of paused list for the given input
        Initial: []
        Add 2: [2]
        Add 1: [1]          --> (removed 2, no need to extend)
        Add 5: [1, 5]       --> (added 5, because it can be extended)
        Add 6: [1, 5, 6]    --> (added 6, because it can be extended)
        Add 2: [1, 2]       --> (removed 6, 5)
        Add 3: [1, 2, 3]    --> (added 3)

    Now if you understand the simulation you can easily visualize
    what's the lower bound of a height should be.

    The lower bound for a height will be the position of the previous
    height from the list who is smaller than that height.
    
    As the list is sorted, it's easy to know where is the previous height
    that is smaller than current height.

    So for simplicity we can keep the position of each height in the
    paused list to know the lower bound of a height easily.

    So now as we can find the lower and upper bound of a height we can easily calculate the area for that height

    Equation is
        height * distance
        height * (upper bound - lower bound + 1)

    Thus we can calculate max area for each height and take the maximum area.
*/

class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> prevMax;
        int ans = 0;
        int len = heights.size();
        for(int i=0; i<len; i++){
            while(!prevMax.empty() && heights[prevMax.top()] > heights[i]){
                int height = heights[prevMax.top()];
                prevMax.pop();

                int lastPos = prevMax.empty() ? -1: prevMax.top();
                int area = height * (i-lastPos-1);
                ans = max(ans, area);
            }
            prevMax.push(i);
        }


        while(!prevMax.empty()){
            int height = heights[prevMax.top()];
            prevMax.pop();

            int lastPos = prevMax.empty() ? -1: prevMax.top();
            int area = height * (len-lastPos-1);
            ans = max(ans, area);
        }

        return ans;
    }
};
