```cpp
// Problem: https://leetcode.com/problems/maximum-depth-of-binary-tree/
// Time: O(N)
// Space: O(N)
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL)
        {
            return 0;
        }
            
        queue<TreeNode*> s;
        s.push(root);
        int res = 0;
        
        while (!s.empty())
        {
            res++;
            int size = s.size();
            while (size--)
            {
                TreeNode* curr = s.front();
                s.pop();
                
                if (curr->left)
                    s.push(curr->left);
                if (curr->right)
                    s.push(curr->right);
            }
           
        }
        
        return res;
    }
};
```