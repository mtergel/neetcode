```cpp
// Problem: https://leetcode.com/problems/subsets-ii
// Time: O(N x 2^N)
// Space: O(N)

class Solution {
private:
    vector<vector<int>> res;
    
    void helper(vector<int>& nums, vector<int>& path, int start)
    {        
        res.push_back(path);
        
        for (int i = start; i < nums.size(); i++)
        {
            // skip duplicates
            if (i > start && nums[i] == nums[i - 1])
            {
                continue;
            }
            
            path.push_back(nums[i]);
            helper(nums, path, i + 1);
            path.pop_back();
        }
    }
    
    
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<int> path;
        helper(nums, path, 0);
        
        return res;
    }
};
```