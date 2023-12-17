```cpp
/**
 ** Solution 1:
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        int len = 0;

        ListNode * temp = head;
        while(temp){
            temp = temp->next;
            len++;
        }
        int targetPos = len-n+1; // need to delete this positions node

        if(targetPos == 1){
            return head->next;
        }

        temp = head;
        // i = 1 because temp is already positioned at 1.
        // we need to delete targetPos. But to do this we need
        // its previous pointer

        // look at the condition. it breaks when i will be at targetPos-1
        for(int i=1; i<targetPos-1; i++){
            temp = temp->next;
        }
        // temp is positined at targetPos-1 position
        temp->next = temp->next->next;

        return head;
    }
};

```


```cpp
/**
Solution 2:
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *prev = nullptr, *temp = head;

        // move temp to n step ahead
        // Note: for each iteration temp is moving forward
        // when i = 1, then temp = head already
        // if a loop succeds then i will be incremented and thus the pointer
        // so if target is 5 then we must continue till i<5.
        // because when i == 5 we must to break loop
        for(int i=1; i<=n; i++){
            temp = temp->next;
        }

        // now temp points to a nth node from start.
        // and prev is n step back.
        if(temp == nullptr){
            return head->next;
        }
        // now prev = 1th pos, temp=nth pos, diff = n-1
        // when temp = last pos, prev = last pos - (n-1) pos
        // now we can delete prev->next because that will point
        // to last_pos-n th position
        prev = head;

        // while temp is not reaching the end.
        while(temp->next){
            temp = temp->next;
            prev=prev->next;
        }
        // now temp = last
        // prev = last-(n-1);
        prev->next = prev->next->next;

        return head;
    }
};
```
