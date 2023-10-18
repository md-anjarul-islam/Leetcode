**Intuition:**
    
    Position:   |0|------------|5|------|10|-------|12|
    Speed:      |100|---------|10|------|20|-------||
    Simulation: |C|------------|B|------|A|--------|target|

Lets say **A, B, C** are three cars and have different speed and are placed in different positions.
And we see **A** is ahead of **B** and has more speed than **B**.

**Observations:**

    1. Can B be a fleet with A? No because A is ahead of B and has higher speed.
    2. Can C be a fleet with A? No. But why!?
    
    Though C has very speed and it is able to be a fleet with A but as its front car is too slow then C will have nothing
    but lowering his speed.
    
    So the main point here is, if there is a slow car at a position then all the preceding cars with higher speed 
    (meets a specific condition) can only be a fleet with that car.
    
    Alternatively if there is a speedy car and there is a slower car in front of that car then there is no way to overtake
    that car.
    
    Only it can be a fleet with the slower car. And then the faster cars speed will slow down and it will become a slower car.
    So the breakpoint is the slower cars.
    
    We need to count the number of slower cars that are unable to be a fleet with its following cars.


**Solution step**
    
    1. Sort the cars by their position.
    2. Start from the car that is near to target because if a car already reaches the target then no other cars 
       (even with highest speed) can't be a fleet with that
    3. Initialize current break point by the car near to target
    4. Iterate over the other cars
        a. Compare the time need to reach the end by the break point car and the current car
        b. If current car requires less time than the brak point car then that car will be a fleet with the current
           break point car
        c. Otherwise the current car (consequently its preceding cars as well) will never be able to a fleet with
           the current break point car.
           And thus it will be considered as a new break point (slow car)
           So, update the current break point by the current car.
           And also increment the total fleets.


**Complexity: O(N logN)**
  
    As we are sorting the list so it will take O(N logN) time.
    And for the iteration we will need a single loop. Though it may seem that we need nested loop, but thats not true.

    Because we are actually maintaining two pointer. Iterating over the array and whenever getting a breakpoint then
    just updating the breakpoint pointer. The update is done in O(1). So the complexity for the iteration is just O(N)
    
    The total complexity is O(N logN) + O(N) which is O(N logN)


**Solution**

    class Solution {
    public:
        int carFleet(int target, vector<int>& position, vector<int>& speed) {
            vector<pair<int,int>> cars;
    
            int len = position.size();
            for(int i=0; i<len; i++){
                cars.push_back({position[i], speed[i]});
            }
    
            sort(cars.begin(), cars.end());
    
            pair<int, int> currFleet = cars[len-1];
            int ans = 1;
    
            for(int i=len-2; i>=0; i--){
                if(
                    (long long)(target-cars[i].first)*currFleet.second >
                    (long long)(target-currFleet.first)*cars[i].second
                ){
                    ans++;
                    currFleet = cars[i];
                }
            }
    
            return ans;
        }
    };
