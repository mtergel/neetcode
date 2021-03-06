```cpp
// Problem: https://leetcode.com/problems/unique-paths
// Time: O(NM)
// Space: O(NM)

class Solution {
public:
    int uniquePaths(int m, int n) {
        // here dp[i][j] means
        // the number of unique paths at [i][j]
        vector<vector<int>> dp(m, vector(n, 1));
        for (int i = 1; i < m; i++)
        {
            for (int j = 1; j < n; j++)
            {
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
            }
        }
        
        return dp[m - 1][n - 1];
    }
};
```