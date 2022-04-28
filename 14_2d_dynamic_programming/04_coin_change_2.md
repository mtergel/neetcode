```cpp
// Problem: https://leetcode.com/problems/coin-change-2
// Time: O(NM)
// Space: O(N)

class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        if (amount == 0)
        {
            return 1;
        }

        if (n == 0)
        {
            return 0;
        }

        vector<int> dp(amount + 1, 0);
        dp[0] = 1;

        for (int i = n - 1; i >= 0; i--)
        {
            vector<int> nextDp(amount + 1, 0);
            nextDp[0] = 1;

            for (int a = 0; a <= amount; a++)
            {
                nextDp[a] = dp[a];
                if (a - coins[i] >= 0)
                {
                    nextDp[a] += nextDp[a - coins[i]];
                }
            }

            dp = nextDp;
        }

        return dp[amount];
    }
};
```