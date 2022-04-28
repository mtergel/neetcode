```cpp
// Problem: https://leetcode.com/problems/word-break/
// Time: O(N^2 * M)
// Space: O(N)

class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.size();
        
        vector<int> dp(n + 1, false);
        dp[n] = true; // goal
        
        for (int i = n - 1; i >= 0; i--) // O(N)
        {
            for (auto w : wordDict) // O(N)
            {
                if ((i + w.size()) <= n 
                    && 
                    s.substr(i, w.size()).compare(w) == 0) // O(N) cause of compare
                {
                    dp[i] = dp[i + w.size()];

                    // can break from dp[i] to dp[n]
                    if (dp[i])
                    {
                        break;
                    }
                }
            }
        }
        
        return dp[0];
    }
};
```