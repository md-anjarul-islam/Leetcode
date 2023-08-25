Intution:
    Merging two triplets makes the new triplet where all the values will be the max among them.
    I can't merge partially. That means while merging i'll have to take the full triplet and take maximum of all the values.
    If a triplet has a number at a position which is greater than the target triplet position can we merge that?
    No. Because if we merge two triplet it always increases. We can't decrease them later. So we can't merge such triplets which has greater value than the target.
    Now on the other side, can we merge a triplet which has some less value than the target?
    If we merge, does the smaller value has any effect on the merging?
    No, because we've already merged a higher value. now merging lower value has no effect. But has one benefit. If there is a number which is equal to the target value than it will be helpful to get the result.
    SO we will merge only those triplets which has lower or equal value with the target

```
class Solution {
public:
    bool mergeTriplets(vector<vector<int>>& triplets, vector<int>& target) {
        
        vector<int> matched(3, 0);

        for(vector<int> &triplet: triplets){
            bool canTake = true;

            for(int i=0; i<3; i++){
                if(triplet[i] > target[i]){
                    canTake = false;
                    break;
                }
            }

            if(canTake == false){
                continue;
            }
            for(int i=0; i<3; i++){
                matched[i] = max(matched[i], triplet[i]);
            }
        }

        for(int i=0; i<3; i++){
            if(matched[i] != target[i]){
                return false;
            }
        }

        return true;
    }
};
```
