```cpp
// Problem: https://leetcode.com/problems/invert-binary-tree/
// Time: O(N)
// Space: O(N)
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL)
        {
            return root;
        }
        
        stack<TreeNode*> s;
        TreeNode* tmp;
        s.push(root);
        
        while (!s.empty())
        {
            int size = s.size();
            while (size--)
            {
                TreeNode* curr = s.top();
                s.pop();
                
                if (curr->left)
                {
                    s.push(curr->left);
                }
                
                if (curr->right)
                {
                    s.push(curr->right);
                }
                
                tmp = curr->left;
                curr->left = curr->right;
                curr->right = tmp;
            }
            
        }
        
        return root;
    }
};
```