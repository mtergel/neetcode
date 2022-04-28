```cpp
// Problem: https://leetcode.com/problems/target-sum
// Time: O(N * t)
// Space: O(N)

class Solution {
private:
    // index, sum, ways
    // "index-sum"
    unordered_map<string, int> dp;
    int helper(vector<int>& nums, int target, int index, int sum)
    {
        // base
        if (index == nums.size())
        {
            if (sum == target)
            {
                return 1;
            }
            return 0;
        }
        
        // memo
        string key = to_string(index) + "-" + to_string(sum);
        if (dp.find(key) != dp.end())
        {
            return dp[key];
        }
        
        dp[key] = helper(nums, target, index + 1, sum + nums[index]) + helper(nums, target, index + 1, sum - nums[index]);
        
        return dp[key];
    }
    
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        return helper(nums, target, 0, 0);
    }
};


// O(2^n) solution

// private:
//     int res = 0;
//     int sum;
//     void helper(vector<int>& nums, int curr, int currSum)
//     {
//         if (curr == nums.size())
//         {
//             if (currSum == sum)
//             {
//                 res++;
//             }
//             return;
//         }
        
//         helper(nums, curr + 1, currSum + nums[curr]);
//         helper(nums, curr + 1, currSum - nums[curr]);
//     }
// public:
//     int findTargetSumWays(vector<int>& nums, int target) {
//         sum = target;
//         helper(nums, 0, 0);
        
//         return res;
//     }
// };
```