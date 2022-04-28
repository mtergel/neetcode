```cpp
// Problem: https://leetcode.com/problems/longest-palindromic-substring
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int numDecodings(string s) {
        int n = s.size();
        vector<int> dp(n + 1, 0);
        dp[n] = 1;
        
        for (int i = n - 1; i >= 0; i--)
        {
            // by itself
            // 26 -> 2 -> B
            if (s[i] != '0')
            {
                dp[i] += dp[i + 1];
            }
            
            // if its an two digit number
            // e.g 26 -> z
            
            if (i + 1 < n &&
               (s[i] == '1' || (s[i] == '2' && s[i + 1] < '7'))
               )
            {
                dp[i] += dp[i + 2];
            }
        }
        
        return dp[0];
    }
};
```