```cpp
// Problem: https://leetcode.com/problems/balanced-binary-tree/
// Time: O(N)
// Space: O(N), O(logN) at best

class Solution {
public:
    bool isBalanced(TreeNode* root) {
       return getDepth(root) != -1;
    }
    
    // -1 means not balanced
    // returns non negative int of height
    int getDepth(TreeNode* curr)
    {
        if (curr == NULL)
        {
            return 0;
        }
        
        int leftHeight = getDepth(curr->left);
        if (leftHeight == -1)
        {
            return -1;
        }
        
        int rightHeight = getDepth(curr->right);
        if (rightHeight == -1)
        {
            return -1;
        }
        
        if (abs(leftHeight - rightHeight) > 1)
        {
            return -1;
        }
        
        return max(leftHeight, rightHeight) + 1;
    }
};
```