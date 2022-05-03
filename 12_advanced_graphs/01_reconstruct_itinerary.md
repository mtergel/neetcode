```cpp
// Problem: https://leetcode.com/problems/min-cost-to-connect-all-points/
// Time: O(E + logE) ?


class Solution {
private:
    unordered_map<string, multiset<string>> adj;
    void dfs(vector<string>& res, string& node)
    {
        
        if (adj.find(node) == adj.end() || adj[node].empty())
        {
            res.push_back(node);
            return;
        }
        
        while (!adj[node].empty())
        {
            string dest = *adj[node].begin();
            adj[node].erase(adj[node].begin());
            
            dfs(res, dest);
        }
        
        res.push_back(node);
    }
    
public:
    vector<string> findItinerary(vector<vector<string>>& tickets) {
        
        for (vector<string>& ticket : tickets)
        {
            adj[ticket[0]].insert(ticket[1]);
        }
        
        vector<string> res;
        string startNode = "JFK";
        
        dfs(res, startNode);
        
        reverse(res.begin(), res.end());
        return res;
    }
};
```