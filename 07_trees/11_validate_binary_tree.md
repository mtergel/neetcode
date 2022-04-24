```cpp
// Problem: https://leetcode.com/problems/validate-binary-search-tree/
// Time: O(N)
// Space: O(N)

class Solution {
private:
    bool checkNode(TreeNode* curr, TreeNode* maxval, TreeNode* minval)
    {
        if (curr == nullptr)
        {
            return true;
        }
        
        if ((minval == nullptr || curr->val > minval->val) && 
            (maxval == nullptr || curr->val < maxval->val))
        {
            return checkNode(curr->left, curr, minval) && checkNode(curr->right, maxval, curr);
        }
        
        return false;
    }
    
public:
    bool isValidBST(TreeNode* root) {
        if (root == nullptr)
        {
            return true;
        }
        
        return checkNode(root, nullptr, nullptr);
    }
    
};
```