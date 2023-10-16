    /**
     * Definition for singly-linked list.
     * struct ListNode {
     *     int val;
     *     ListNode *next;
     *     ListNode() : val(0), next(nullptr) {}
     *     ListNode(int x) : val(x), next(nullptr) {}
     *     ListNode(int x, ListNode *next) : val(x), next(next) {}
     * };
     */
    class Solution {
    public:
        void reorderList(ListNode* head) {
            vector<ListNode*> nodes;
    
            ListNode* ptr = head;
    
            while(ptr!=NULL){
                nodes.push_back(ptr);
                ptr = ptr->next;
            }
    
            int len = nodes.size();
    
            ptr = nodes[0];
            int l = 1, r = nodes.size()-1;
    
            while(l<=r){
    
                ptr->next = nodes[r--];
                ptr = ptr->next;
    
                if(l > r){
                    break;
                }
                ptr->next = nodes[l++];
                ptr = ptr->next;
            }
            ptr->next = NULL;
        }
    };
