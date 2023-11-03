```cpp
/**
    BFS on tree
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;

        if(!root){
            return ans;
        }

        queue<TreeNode*> q;

        q.push(root);

        while(!q.empty()){
            int len = q.size();
            vector<int> levelNodes;

            for(int i=0; i<len; i++){
                // pick the node in front of the queue
                TreeNode* node = q.front();
                // remove that node as processed
                q.pop();

                levelNodes.push_back(node->val);
                if(node->left != NULL){
                    q.push(node->left);
                }
                if(node->right != NULL){
                    q.push(node->right);
                }
            }

            ans.push_back(levelNodes);
        }

        return ans;
    }
};
```
