**Intuition:**

When initiating our journey from the **i'th** station, we collect **gas[i]** and consume **cost[i]**, resulting in a net gain denoted as **gain[i] = gas[i] - cost[i]**.

Therefore, embarking from station **i** and proceeding onwards allows us to accumulate gas along the way. If, at any station, the total gain becomes negative, we can not move to the next station.

A simplistic approach would involve starting from any station and calculating the overall gain. If, at any station, the accumulated gain turns negative, we must reconsider our starting point. Consequently, we try again from the next station.

```c
for(int i=0; i<len; i++){
    totalGas = 0;
    for(int j=i; j<len; j++){
        totalGas+=(gas[i]-cost[i]);
        if(totalGas < 0 ){
            break;
        }
    }
    
    if(totalGas > 0){
        // validate the entire cycle starting from i.
        return i;
    }
}
```

Nevertheless, this solution exhibits a time complexity of O(N^2), which we aim to optimize.

So, should we start our journey from the station immediately succeeding the prior one? Or could we skip multiple stations at once?

The answer "we will skip all the stations up to the station where we encountered negative gain". But why this should work?

Consider two test cases, (focusing solely on the gain values.)

**Case 1:**

Gain = [2, 5, 3, -11]

Starting from the first index, the total gain is 2+5+3+(-11) = -1. Hence, **2** cannot be the starting station as we got negative total.

Now, should we initiate our journey from the next station (gain 5)? One might assume that as we've started with smaller gain that's why the total gain became negative.  However, since there are larger gain values subsequent to this point, it's plausible to consider them as potential starting stations. Is this assumption accurate?

No, it isn't. Why? Because regardless of where we started our journey (smaller/larger gain), as we progress through the stations, we accumulate both the smaller and larger gains in the total gain. If this total gain (including the larger gains) doesn't suffice to offset the greater negative gain, then starting from the next station won't make any difference. This is due to the fact that initiating from the next station would mean losing some gain (albeit a small amount, but it's still a loss). This holds true for any other station within that range.

**Case 2:**

Gain = [2, -12, 5, 4]

Here, the total gain is 2+(-12)+5+4 = -1. Consequently, **2** cannot be the starting station, and we should skip the entire range.

However, this assumption is incorrect! The algorithm dictates that if the total gain becomes negative at any point, we should reset the total to 0. Let's simulate this:

Gain = [2, -12, 5, 4]

Total = 2, -10 | 5, 9 (the | symbol splits the array)

Therefore, the previous scenario where the **total gain = -1** will never occur.

Understanding this point is crucial because the algorithm effectively divides the array into segments, and if the sum of any segment becomes negative, a new segment begins.

**Solution**
```cpp
    class Solution {
    public:
        int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
            
            int reserve = 0, len = gas.size(), ans = 0, totalReserve = 0;
    
            for(int i=0; i<len; i++){
                
                reserve+=(gas[i]-cost[i]);
                totalReserve+=(gas[i]-cost[i]);
    
                if(reserve<0){
                    // If reserve < 0 then the total previous segment is bad
                    // previous Segment = [previous starting index, i]
    
                    // retry from the next index
                    reserve = 0;
                    ans = i+1;
                }
            }
    
            // if total reserve < 0 then round trip is never possible
            return totalReserve < 0 ? -1 : ans;
        }
    };
```
