```cpp
/**
    Intution:
    Let's say there is a path from root [root, A, B, C, X]
    And the values are [v0, v1, v2, v3, v4]

    For X, to be a good node the following condition must be true
       => (v4 >= v0 & v4>=v1 & v4>=v2 & v4>=v3)
       => v4 >= max([v0, v1, v2, v3])

    So rather than comparing with each value we can take the max value
    among them and compare to identify good node

 */
class Solution {
public:
    int ans=0;

    void solve(TreeNode* root, int currentMax=INT_MIN){
        if(!root){
            return;
        }
        if(root->val >= currentMax){
            ans++;
        }

        // update currenet max value
        currentMax = max(currentMax, root->val);

        solve(root->left, currentMax);
        solve(root->right, currentMax);
    }
    int goodNodes(TreeNode* root) {
        solve(root);

        return ans;
    }
};
```
