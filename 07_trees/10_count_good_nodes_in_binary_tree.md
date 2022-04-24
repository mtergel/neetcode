```cpp
// Problem: https://leetcode.com/problems/count-good-nodes-in-binary-tree/
// Time: O(N)
// Space: O(N)

class Solution {
private:
    int findGoodNodes(TreeNode* curr, int maxVal)
    {
        if(!curr) return 0;

        int goodNode = 0;
        if(curr->val >= maxVal)
        {
            maxVal = curr->val;
            goodNode++;
        }

        return goodNode + findGoodNodes(curr->left, maxVal) + findGoodNodes(curr->right, maxVal);
    }
    
public:
    int goodNodes(TreeNode* root) {
        if (root == nullptr)
        {
            return 0;
        }
        
        return findGoodNodes(root, root->val);
    }
};
```