```cpp
// Problem: https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    
    int preorderIndex = 0;
    unordered_map<int, int> inorderIndex;
    
    TreeNode* helper(vector<int>& preorder, int left, int right)
    {
        if (left > right)
        {
            return nullptr;
        }
        
        int rootVal = preorder[preorderIndex];
        preorderIndex++;
        
        TreeNode* root = new TreeNode(rootVal);
        
        root->left = helper(preorder, left, inorderIndex[rootVal] - 1);
        root->right = helper(preorder, inorderIndex[rootVal] + 1, right);
        
        return root;
    }
    
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        
        for (int i = 0; i < inorder.size(); i++)
        {
            inorderIndex[inorder[i]] = i;
        }
        
        return helper(preorder, 0, preorder.size() - 1);
    }
};
```