```cpp
// Problem: https://leetcode.com/problems/kth-smallest-element-in-a-bst/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        int res = 0;
        
        stack<TreeNode*> stck;
        TreeNode* curr = root;
        
        while (!stck.empty() || curr)
        {
            while (curr)
            {
                stck.push(curr);
                curr = curr->left;
            }
            
            curr = stck.top();
            stck.pop();
            
            if (--k == 0)
            {
                return curr->val;
            }
            
            curr = curr->right;
        }
        
        return res;
    }
};
```