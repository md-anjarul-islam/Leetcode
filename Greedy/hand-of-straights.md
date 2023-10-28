```cpp
/**

    Observations:
    1. Each card must be in a group
    2. As the cards should be consecutive that means they must be sorted in that group
    3. So based on these we can start from the smallest integer and try finding consecutives until the group is fulfilled
    4. We can take map so that the cards are sorted by their key.
    But as there could be duplicate numbers so we should consider the count of each number/key
*/

class Solution {
public:
    bool isNStraightHand(vector<int>& hand, int groupSize) {
        map<int, int> freqMap;

        // if equal division is not possible then answer is false
        if(hand.size()%groupSize){
            return false;
        }

        for(int h: hand){
            freqMap[h]++;
        }

        int totalGroup = hand.size()/groupSize;
        for(int i=0; i<totalGroup; i++){
            // take the current smallest key to form a group
            int card = freqMap.begin()->first; 
            
            for(int j=0; j<groupSize; j++){
                if(freqMap.find(card) == freqMap.end()){
                    return false;
                }

                // card has been taken. so decrement count
                freqMap[card]--;
            
                // if all cards are taken then delete the card so that on
                // next iteration we can start with available smallest key
                if(freqMap[card] == 0){
                    freqMap.erase(card);
                }

                card++;
            }
        }
        
        return true;
    }
};
```
