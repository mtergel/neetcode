```cpp
// Problem: https://leetcode.com/problems/subsets
// Time: O(N ^ k)
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
            path.push_back(nums[i]);
            sum += nums[i];
            
            // dont go to next number
            // since each num can be used unlimited number of times
            helper(nums, path, sum, i);
            
            sum -= nums[i];
            path.pop_back();
        }
        
    }
    
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
     
        target_sum = target;
        vector<int> path;
        helper(candidates, path, 0, 0);
        return res;
    }
};
``` 