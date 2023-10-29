**Observation:**
  The problem clearly describes that a letter can't appear in multiple parts.
  So if a letter is taken then we need to know the last occurrence of that letter.
  We must take all of those letters.
  And if any other letter in that range occurs later after the range then we
  need to reconsider that as end of the range.

  So we can iterate from the last and take the maximum index of a letters occurence.

  Then start from the first letter, set the end as the last occurence of that letter
  continue up to that index. Also check the other letters last occurence in that range
  and adjust the final end accordingly.


```cpp
class Solution {
public:
    vector<int> partitionLabels(string s) {
        
        vector<int> lastOccurrence(26, -1), ans;
        int len = s.size();

        for(int i=len-1; i>=0; i--){
            // calculate the last occurrence of a letter
            if(lastOccurrence[s[i]-'a'] == -1)
                lastOccurrence[s[i]-'a'] = i;
        }

        int currentLast = 0;
        int partLen = 0;

        for(int i=0; i<len; i++){

            // adjust the end of the current partition
            currentLast = max(currentLast, lastOccurrence[s[i]-'a']);
            partLen++;
            // if the end of the partition is reached 
            if(i == currentLast){
                ans.push_back(partLen);
                partLen = 0;
            }
        }

        return ans;
    }
};
```
