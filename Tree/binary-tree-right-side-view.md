```cpp
/**
    Observation:
    If the right subtree has more height then the left subtree then the
    answer should be always the right subtrees nodes start from root.

    But if the height is less then the left subtree then we need to take
    some nodes from other subtree as well

    So if we closely look into the problem
    - looking from right side we will only be able to see exactly one
      node at each level
    - so we can traverse the tree and take the node for each level
    - we will visit from the left to right and whenever will get a node
      at a level we will overwrite that levels node by the newest node.
      as we are going from left to right so finally the rightmost nodes
      at each level will be remaining
 */
class Solution {
    vector<int> ans;
    void visit(TreeNode* root, int level){
        if(!root){
            return;
        }

        // update the node at this level
        if(level < ans.size()){
            ans[level] = root->val;
        }
        // otherwise insert the node at this level
        else{
            ans.push_back(root->val);
        }

        // visit left subtree first and then right subtree
        visit(root->left, level+1);
        visit(root->right, level+1);
    }
public:
    vector<int> rightSideView(TreeNode* root) {
        visit(root, 0);

        return ans;
    }
};
```
