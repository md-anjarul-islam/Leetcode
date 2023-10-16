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
        int maxDepth(TreeNode* root) {
            // Edge case
            if(!root) return 0;
    
            // recursively calculate the depth of the left & right subtree
            // take the max of them
            
            // Length of (current node) + (it's max_subtree)
            // => 1 + (max sub tree length)
            return 1+max(maxDepth(root->left), maxDepth(root->right));
        }
    };
