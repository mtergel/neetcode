```cpp
// Problem: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown
// Time: O(N)
// Space: can be reduced to O(1) 

class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        
        // profit when
        
        // we dont have any stocks
        vector<int> s0(n, 0);
        
        // we have stock
        vector<int> s1(n, 0);
        
        // we sold stock
        vector<int> s2(n, 0);        
        
        s0[0] = 0; // no stocks
        s1[0] = -prices[0]; // current profit after you buy the first stock
        s2[0] = INT_MIN; // didnt sell any stocks yet
        
        for (int i = 1; i < n; i++)
        {
            // max the profit
            // by staying at s0, or cooldown from s2
            s0[i] = max(s0[i - 1], s2[i - 1]);
            
            // max the profit
            // by staying at s1, or buying from s0
            s1[i] = max(s1[i - 1], s0[i - 1] - prices[i]);
            
            // can only sell
            s2[i] = s1[i - 1] + prices[i];
        }
        
        return max(s0[n - 1], s2[n - 1]);
    }
};
```