```cpp

class Solution {
    bool ans;

    int solve(TreeNode* root){
        if(!root){
            return 0;
        }

        int leftHeight = solve(root->left);
        int rightHeight = solve(root->right);

        // given condition
        if(abs(leftHeight-rightHeight) > 1) {
            ans = false;
        }

        return 1+max(leftHeight, rightHeight);
    }
public:
    bool isBalanced(TreeNode* root) {
        ans = true;
        solve(root);
        return ans;
    }
};
```
