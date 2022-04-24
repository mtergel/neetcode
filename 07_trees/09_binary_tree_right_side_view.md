```cpp
// Problem: https://leetcode.com/problems/binary-tree-right-side-view/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        if (root == NULL) return res;
        
        queue<TreeNode*> bfs;
        bfs.push(root);
        
        while (!bfs.empty())
        {
            int lvlSize = bfs.size();
            
            for (int i = 0; i < lvlSize; i++)
            {
                TreeNode* curr = bfs.front();
                bfs.pop();
                
                if (i == lvlSize - 1)
                {
                    res.push_back(curr->val);
                }
                
                if (curr->left) bfs.push(curr->left);
                if (curr->right) bfs.push(curr->right);
            }
        }
        
        return res;
    }
};
```