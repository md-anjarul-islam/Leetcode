```cpp
/**
    A path in binary tree can be considered as two subpath passing
    through a root. So for each root we can consider a path like
        - Take non-zero sum of left subpath
        - Take non-zero sum of right subpath
        - Take the current root value
        - Calculate total as (left_path+right_path+curr_root_value)
        - Calculate max
 */
class Solution {
    int ans;

    int solve(TreeNode *root){
        if(!root){
            return 0;
        }

        // left subtree max
        int lmax = max(0, solve(root->left));
        // right subtree max
        int rmax = max(0, solve(root->right));
        // if current root makes the path
        ans = max(ans, lmax+rmax+root->val);

        // return maximum path possible.
        return root->val + max(lmax, rmax);
    }
public:
    int maxPathSum(TreeNode* root) {
        ans = INT_MIN;
        solve(root);
        return ans;
    }
};
```
