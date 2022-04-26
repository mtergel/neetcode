```cpp
// Problem: https://leetcode.com/problems/min-cost-climbing-stairs/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        if (n == 2)
        {
            return min(cost[0], cost[1]);
        }
        
        vector<int> dp(cost);
        
        for (int i = n - 3; i >= 0; i--)
        {
            dp[i] = min(dp[i] + dp[i + 1], dp[i] + dp[i + 2]);
        }
        
        
        return min(dp[0], dp[1]);        
    }
};
```