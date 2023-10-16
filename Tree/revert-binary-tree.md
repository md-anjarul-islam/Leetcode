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
        TreeNode* invertTree(TreeNode* root) {
            // Edge case
            if(root == NULL){
                return root;
            }
    
            // recursively invert the subtrees first
            invertTree(root->left);
            invertTree(root->right);
    
            // now invert the subtree roots
            swap(root->left, root->right);
    
            return root;
        }
    };
