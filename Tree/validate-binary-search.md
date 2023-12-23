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

public:
     // left sub-tree must be in range [lowerLimit, root_value);
     // right sub-tree must be in range (root_value, upperLimit];
    bool isValidBST(TreeNode* root, long long lowerLimit = INT_MIN*2LL, long long upperLimit = INT_MAX*2LL) {
        if(!root)
            return true;
        if(root->val <= lowerLimit || root->val >= upperLimit){
            return false;
        }
        // left sub-tree must be in range [lowerLimit, root_value);
        // right sub-tree must be in range (root_value, upperLimit];
        return isValidBST(root->left, lowerLimit, root->val) && isValidBST(root->right, root->val, upperLimit);
    }
};
```
