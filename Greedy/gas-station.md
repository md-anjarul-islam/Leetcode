**Intuition:**
  
**Observations:**
  
    


**Solution step**
    
   


**Complexity: O(N)**
  
    


**Solution**

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
