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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
private:

    TreeNode* deserializeHelper(istringstream &ss)
    {
        string val;
        ss >> val;

        if (val == "null")
        {
            return nullptr;
        }

        TreeNode* curr = new TreeNode(stoi(val));
        curr->left = deserializeHelper(ss);
        curr->right = deserializeHelper(ss);

        return curr;
    }

public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
       return root == nullptr ? " null" : " " + to_string(root->val) + serialize(root->left) + serialize(root->right);
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        istringstream ss(data);
        return deserializeHelper(ss);
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```