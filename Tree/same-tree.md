**Intution**
  
  To check similarity
   - Both the root node should be the same
   - Also recursively left and right subtree should be the same

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        // if both are null (edge case)
        if(!p && !q) return true;

        // if anyone of them became null then they are not same
        if(!p || !q) return false;

        // if their value are not same then they are not same
        if(p->val != q->val) return false;

        // recursively check left and right subtree
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```
