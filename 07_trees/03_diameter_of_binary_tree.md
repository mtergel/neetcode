```cpp
// Problem: https://leetcode.com/problems/diameter-of-binary-tree/

// Time: O(N)
// Space: O(N)

class Solution {
private:
    int res = 0;
public:
    int calcHeight(TreeNode* curr)
    {
        if (curr == NULL)
        {
            return 0;
        }
        
        int leftHeight = calcHeight(curr->left);
        int rightHeight = calcHeight(curr->right);
        
        res = max(res, leftHeight + rightHeight);
        
        return 1 + max(leftHeight, rightHeight);
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        
        calcHeight(root);
        
        return res;
    }
};
```