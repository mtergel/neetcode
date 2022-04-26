```cpp
// Problem: https://leetcode.com/problems/number-of-provinces
// Time: ~O(N + E)
// Space: O(N + E)

// for some reason I cant code the iterative version

class Solution {
public:
    unordered_set<int> visited;
    vector<vector<int>> adj;
    bool validTree(int n, vector<vector<int>> &edges) {
        if (n == 0)
        {
            return true;
        }

        for (int i = 0; i < n; i++)
        {
            vector<int> t;
            adj.push_back(t);
        }

        for (vector<int> edge : edges)
        {
            adj[edge[0]].push_back(edge[1]);
            adj[edge[1]].push_back(edge[0]);
        }

        return dfs(0, -1) && visited.size() == n;
    }

    bool dfs(int i, int prev) {
        if (visited.find(i) != visited.end())
        {
            return false;
        }
        else
        {
            visited.insert(i);
            for (int j : adj[i])
            {
                if (j == prev)
                {
                    continue;
                }
                if (!dfs(j, i))
                {
                    return false;
                }
            }

            return true;
        }
    }

};
```