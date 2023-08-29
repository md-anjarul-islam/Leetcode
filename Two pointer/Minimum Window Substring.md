# Problem
Given two strings s and t of lengths m and n respectively, return the minimum window 
substring
 of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

# Solution
```
/*
    The problem asks for the finding a window where all the characters of t is present in the window.
    This gives us some insights
        - Character sequence does not matter while comparing
        - All the characters of t should be included in the substring of s
        - Thus all the characters frequency should be >= to the character frequency of s.

        For example, if t = "AAB", then in s there should a substring where there are at least 2 'A' and at least 1 'B' present.
        s = "ABBA" is a valid substring. because there are 2 'A' and more than 1 'B'. so all the characters of t is present in that substring

        So finding a solution in a range is easier using two pointer algorithm.
        Let's say we have two pointer (left and right).

        Step 1: Initialize left and right = 0
        Step 2: move right pointer to the right side. and include the character from s until a match is found.
        Step 3: Check all the characters of s in the current window (left, right).
        match the characters frequency with the character frequency of t.
            Now, possibly the current window can be a match. But that might not be the minimum length.
            For this scenario lets consider a test case
            t = "AB", s = "AAAB"
            in our solution we are proposing to move the right pointer and try matching with t. So here if we start from 0 and then move our right pointer we'll have to move the right pointer

        left = 0, right = 0, target frequency (t) = {"A": 1, "B": 1}
        Iteration 1:
            left = 0, right = 0 frequency (s[0, 0]) = {"A": 1} (didn't match)
        Iteration 2:
            left = 0, right = 1 frequency (s[0, 1]) = {"A": 2} (didn't match)
        Iteration 3:
            left = 0, right = 1 frequency (s[0, 2]) = {"A": 3} (didn't match)
        Iteration 4:
            left = 0, right = 2 frequency (s[0, 3]) = {"A": 3, "B": 1} (matched)
        
        Now we can see we can skip some characters from the left to get the minimum length and also to keep the match

        So now move the left pointer
        Iteration 5:
            left = 1, right = 3 frequency (s[1, 3]) = {"A": 2, "B": 1} (still match)
        Iteration 6:
            left = 2, right = 3 frequency (s[2, 3]) = {"A": 1, "B": 1} (still match)
        
        Iteration 7:
            left = 3, right = 3 frequency (s[3, 3]) = {"B": 1} (didn't match)
        
        So the last range was the minimum.
        So in each iteration we can calculate the length and compare to get the minimum length.

        This way finally we will get the optimal answer.
*/
class Solution {
public:
    string minWindow(string s, string t) {
        
        unordered_map<char, int> sFreq, tFreq;
        // count the number of unique characters in t.
        int uniqueChars = 0;
        for(char c: t){
            tFreq[c]++;
            if(tFreq[c] == 1)
                uniqueChars++;
        }

        // loop through the string. 
        int left = 0, right = 0, len = s.size(), matchedChars=0;
        int ans = INT_MAX;
        int leftPos = 0;
        while(right<len){

            char rcc = s[right];
            sFreq[rcc]++;
            right++;

            if(sFreq[rcc] == tFreq[rcc]){
                matchedChars++;
            }

            while(left<right && matchedChars == uniqueChars){
                if(ans > (right-left)){
                    ans = right-left;
                    leftPos = left;
                }

                char lcc = s[left];
                if(sFreq[lcc] == tFreq[lcc]){
                    matchedChars--;
                }
                left++;
                sFreq[lcc]--;
            }
        }

        if(ans == INT_MAX)
            return "";
        
        else 
            return s.substr(leftPos, ans);
    }
};
```
