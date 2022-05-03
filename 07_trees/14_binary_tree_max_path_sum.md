```cpp
// Problem: https://leetcode.com/problems/binary-tree-maximum-path-sum/
// Time: O(N)
// Space: O(N) for callstack

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
private:
    int res = INT_MIN;
    int findSum(TreeNode* curr)
    {
        if (curr == nullptr)
        {
            return 0;
        }
        
        // find the sums of the left/right half
        int leftSum = findSum(curr->left);
        int rightSum = findSum(curr->right);
        
        // we are trying to find the maximum
        // so ignore negative sums
        leftSum = max(leftSum, 0);
        rightSum = max(rightSum, 0);
        
        // update res
        // are allowed to split
        // max sum running through this node
        res = max(res, leftSum + curr->val + rightSum);
        
        // return up to callstack
        // the max sum of the current node
        return max(leftSum, rightSum) + curr->val;
    }
    
public:
    int maxPathSum(TreeNode* root) {
        findSum(root);
        
        return res;
    }
};
```