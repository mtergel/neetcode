```cpp
// Problem: https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
// Time: O(logN)
// Space: O(1)
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL)
        {
            return root;
        }
        
        if (root->val > p->val && root->val > q->val)
        {
            return lowestCommonAncestor(root->left, p, q);
        }
        
        if (root->val < p->val && root->val < q->val)
        {
            return lowestCommonAncestor(root->right, p, q);
        }
        
        return root;
    }
};
```