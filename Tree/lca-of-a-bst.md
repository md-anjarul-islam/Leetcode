```cpp
/**
    As this is a BST so search like binary search.

    The LCA should be the first node where given two values
    are splitted into two sub tree.

    So recursively search
    - If both given values are one sided then search that side
    - When they are on different side then return the node
 */

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root){
            return nullptr;
        }

        // search on left tree
        if(max(p->val, q->val) < root->val){
            return lowestCommonAncestor(root->left, p, q);
        }

        // search on right tree
        else if(min(p->val, q->val) > root->val){
            return lowestCommonAncestor(root->right, p, q);
        }

        // the LCA must be the current root
        // because this is the node where p & q are not
        // on the same side. that means they are on
        // two different side of the current node.
        return root;
    }
};
```
