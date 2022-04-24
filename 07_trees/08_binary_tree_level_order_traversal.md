```cpp
// Problem: https://leetcode.com/problems/binary-tree-level-order-traversal
// Time: O(N)
// Space: O(N)

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (root == nullptr)
        {
            return res;
        }
        
        queue<TreeNode*> bfs;
        bfs.push(root);
        
        while (!bfs.empty())
        {
            int size = bfs.size();
            vector<int> level;
            while (size--)
            {
                TreeNode* curr = bfs.front();
                bfs.pop();
                
                level.push_back(curr->val);
                
                if (curr->left)
                {
                    bfs.push(curr->left);
                }
                
                if (curr->right)
                {
                    bfs.push(curr->right);
                }
            }
            
            res.push_back(level);
        }
        
        return res;
    }
};
```