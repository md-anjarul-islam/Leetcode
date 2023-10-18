**Intuition:**
   Diameter of a tree is the maximum distance any two nodes of the tree.
   Traverse through the tree. From a node take it's left subtree and 

**Solution step**
    
    1. Traverse the tree recursively
    2. Calculate the max length of the left and right sub tree
    3. Calculate the diameter length possible from the current node
    4. Choose only the max subtree (left/right) possible from the current node to
       calculate the diameter of its parent node..

**Complexity: O(N)**
  

**Solution**

  class Solution {
      int ans;
  
      int solve(TreeNode* root) {
          // The base case
          if(!root)  return 0;
  
          int leftMax = solve(root->left); // max depth of left sub tree
          int rightMax = solve(root->right); // max depth of right sub tree
  
          /* consider the max diameter is the path between the left max subtree and 
           the right sub tree. so while considering any subtree we are
           taking the max path length of that subtree.
           and also as the path goes through the root so 1 should be added
          */
  
          ans = max(ans, 1 + leftMax + rightMax);
  
          /* if this diameter is not the best one then we are going back
          from the current root. while going back we will take the max
          sub tree from the current root. because we can't take both
          path.
          if we go one step up (the parent of root), then possibly the current
          roots max path can be one part of the diameter.
          */
          return 1 + max(leftMax, rightMax);
      }
    public:
        int diameterOfBinaryTree(TreeNode* root) {
            // The base case
            if(!root)  return 0;
            solve(root);
            /*
                Note: So far we've calculated the length of the diameter. But we
                need the distance between them.
                For simple explanation
                A->B has length 2. But distance between A to B is 1.
                A->B->C has length 3, but distance between A to C is 2.
            */
            return ans-1;
        }
    };
