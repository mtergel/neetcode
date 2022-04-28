```cpp
// Problem: https://leetcode.com/problems/cheapest-flights-within-k-stops/
// Time: O(N + E logN)
// Space: O(N + E)

class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<int> prices(n, INT_MAX);
        prices[src] = 0;
        
        for (int i = 0; i < k + 1; i++)
        {
            vector<int> tmpPrice(prices.begin(), prices.end());
            for (auto flight : flights)
            {
                int from = flight[0];
                int to = flight[1];
                int price = flight[2];
                
                if (prices[from] == INT_MAX)
                {
                    continue;
                }
                
                if (prices[from] + price < tmpPrice[to])
                {
                    tmpPrice[to] = prices[from] + price;
                }
            }
            prices = tmpPrice;
        }
        
        return prices[dst] == INT_MAX ? -1 : prices[dst];
    }
};
```