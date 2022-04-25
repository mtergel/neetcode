```cpp
// Problem: https://leetcode.com/problems/subsets
// Time: O(N!)
// Space: O(N)

class Solution {
private:
    vector<vector<int>> res;
    
    void helper(vector<int>& nums, int start) {
        if (start == nums.size() - 1)
        {
            res.push_back(nums);
            return;
        }
        
        for (int i = start; i < nums.size(); i++)
        {
            swap(nums[i], nums[start]);
            helper(nums, start + 1);
            swap(nums[i], nums[start]);
        }
            
    }
    
public:
    vector<vector<int>> permute(vector<int>& nums) {
        helper(nums, 0);
        
        return res;
    }
};
``` 