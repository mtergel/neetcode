```cpp
// Problem: https://leetcode.com/problems/word-break/
// Time: O(N logN)
// Space: O(N)

class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        // O(n)
        
        vector<int> sorted;
        for (int num : nums)
        {
            if (sorted.empty() || sorted.back() < num)
            {
                sorted.push_back(num);
            }
            else
            {
                auto it = lower_bound(sorted.begin(), sorted.end(), num);
                *it = num;
            }
        }
        
        return sorted.size();
        
//         int n = nums.size();
//         if (n == 1)
//         {
//             return 1;
//         }
        
//         vector<int> dp(n, 1);
//         int res = 1;
        
//         for (int i = n - 1; i >= 0; i--)
//         {
//             for (int j = n + 1; j < n; j++)
//             {
//                 if (nums[i] < nums[j])
//                 {
//                     dp[i] = max(dp[i], 1 + dp[j]);
//                     res = max(res, dp[i]);
//                 }
//             }
//         }
            
//         return res;
    }
};
```