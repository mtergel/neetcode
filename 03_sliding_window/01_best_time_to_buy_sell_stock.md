```cpp
// Problem: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
// Time: O(N)
// Space: O(1)
// Note: Kadane's Algorithm, Max Subarray Problem
// If they are negative numbers in input
// reset it to 0 if it falls down to negaitve

class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.size() == 1)
        {
            return 0;
        }            
            
        int profit = 0;
        int toBuy = prices[0];
        for (int i = 1; i < prices.size(); i++)
        {
            profit = max(profit, prices[i] - toBuy);
            toBuy = min(toBuy, prices[i]);
        }
        
        return profit;
    }
};
```