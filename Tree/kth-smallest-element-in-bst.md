```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    int getSize(TreeNode* root){
        if(!root){
            return 0;
        }

        return 1+getSize(root->left)+getSize(root->right);
    }

public:
    int kthSmallest(TreeNode* root, int k) {
        int leftSize = getSize(root->left);
        int rightSize = getSize(root->right);
        
        if(k == leftSize+1){
            return root->val;
        }

        if(k<=leftSize){
            return kthSmallest(root->left, k);
        }
        else{
            return kthSmallest(root->right, k-leftSize-1);
        }
    }
};
```
