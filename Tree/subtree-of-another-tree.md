```cpp
/**
    Brute force:
    - Recursively visit the tree
    - Compare the visiting subtree with the given subtree
*/
class Solution {
    bool isSame(TreeNode* root, TreeNode* subRoot){
        if(!root && !subRoot){
            return true;
        }

        if(!root || !subRoot){
            return false;
        }

        // if they are identical both by value and structure
        return root->val == subRoot->val && isSame(root->left, subRoot->left) && isSame(root->right, subRoot->right);
    }
    bool ans = false;
public:
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {

        if(!root){
            return false;
        }

        // if ans is already true or the current subtree is same or its left or right child recursively..
        return ans = ans || isSame(root, subRoot) || isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot);
    }
};
```
