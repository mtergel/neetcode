```cpp
// Problem: https://leetcode.com/problems/longest-increasing-path-in-a-matrix
// Time: O(NM)
// Space: O(NM)

class Solution {
private:
    vector<vector<int>> dp;
    int m, n;
    
    int res = 0;
    
    int dfs(int i, int j, int prev, vector<vector<int>>& matrix)
    {
        if (i < 0 || i == m || j < 0 || j == n || matrix[i][j] <= prev)
        {
            return 0;
        }
        
        if (dp[i][j] != -1)
        {
            return dp[i][j];
        }
        
        int count = 1;
        count = max(count, 1 + dfs(i + 1, j, matrix[i][j], matrix));
        count = max(count, 1 + dfs(i - 1, j, matrix[i][j], matrix));
        count = max(count, 1 + dfs(i, j + 1, matrix[i][j], matrix));
        count = max(count, 1 + dfs(i, j - 1, matrix[i][j], matrix));
        
        dp[i][j] = count;
        res = max(res, dp[i][j]);
        
        return count;
    }
    
public:
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        m = matrix.size();
        n = matrix[0].size();
        
        dp.resize(m, vector(n, -1));
        
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dfs(i, j, -1, matrix);
            }
        }
        
        return res;
    }
};
```