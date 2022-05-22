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
        
        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty())
        {
            int size = q.size();
            while (size--)
            {
                TreeNode *curr = q.front();
                q.pop();

                if (curr->left)
                {
                    q.push(curr->left);
                }

                if (curr->right)
                {
                    q.push(curr->right);
                }

                swap(curr->left, curr->right);
            }
        }
        
        return root;
    }
};
```