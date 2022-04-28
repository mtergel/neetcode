```cpp
// Problem: https://leetcode.com/problems/interleaving-string/
// Time: O(NM)
// Space: O(NM)

class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        // s3's pointers position = s1's pointer + s2's pointer
        
        int m = s1.size();
        int n = s2.size();
        
        if (s3.size() != m + n)
        {
            return false;
        }
        
        vector<vector<bool>> dp(m + 1, vector(n + 1, false));
        dp[m][n] = true;
        
        for (int i = m; i >= 0; i--)
        {
            for (int j = n; j >= 0; j--)
            {
                if (i < m && s1[i] == s3[i + j] && dp[i + 1][j])
                {
                    dp[i][j] = true;
                }
                
                if (j < n && s2[j] == s3[i + j] && dp[i][j + 1])
                {
                    dp[i][j] = true;
                }
            }
        }
        
        
        return dp[0][0];
    }
}; 
```