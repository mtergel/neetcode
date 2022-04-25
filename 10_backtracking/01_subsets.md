```cpp
// Problem: https://leetcode.com/problems/subsets
// Time: O(N x 2^N)
// Space: O(N)

class Solution {
private:
    vector<vector<int>> res;
    void helper(vector<int>& nums, int start, vector<int>& path) {
        if (start == nums.size())
        {
            res.push_back(path);
            return;
        }
        
        path.push_back(nums[start]);
        helper(nums, start + 1, path);
        
        path.pop_back();
        helper(nums, start + 1, path);
    };
    
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        
        vector<int> path;
        helper(nums, 0, path);
        
        return res;
    }
};
```