```cpp
// Problem: https://leetcode.com/problems/coin-change
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        // max value is amout + 1
        
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;
        
        for (int i = 1; i <= amount; i++)
        {
            for (int coin : coins)
            {
                if (i >= coin)
                {
                    dp[i] = min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        
        return dp[amount] != amount + 1 ? dp[amount] : -1;
    }
};
```