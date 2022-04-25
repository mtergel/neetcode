```cpp
// Problem: https://leetcode.com/problems/subsets-ii
// Time: O(N x 2^N)
// Space: O(N)

class Solution {
private:
    vector<vector<int>> res;
    int target_sum;
    
    void helper(vector<int>& nums, vector<int>& path, int sum, int start) 
    {
        if (sum >= target_sum)
        {
            if (sum == target_sum)
            {
                res.push_back(path);
            }
            
            return;
        }
        
        for (int i = start; i < nums.size(); i++)
        {
            if (i > start && nums[i] == nums[i - 1])
            {
                continue;
            }
            
            path.push_back(nums[i]);
            sum += nums[i];
            
            helper(nums, path, sum, i + 1);
            
            path.pop_back();
            sum -= nums[i];
        }
            
    }
    
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        target_sum = target;
        vector<int> path;
        
        sort(candidates.begin(), candidates.end());
        helper(candidates, path, 0, 0);
        
        return res;
    }
};
```