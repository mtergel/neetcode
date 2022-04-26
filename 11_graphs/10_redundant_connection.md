```cpp
// Problem: https://leetcode.com/problems/rotting-oranges
// Time: ~O(N)
// Space: O(N)

class Solution {
private:
    vector<int> parent;
    vector<int> ranks;
    
    int find(int x)
    {
        if (parent[x] == x)
        {
            return x;
        }
        
        // path compression
        parent[x] = find(parent[x]);
        return parent[x];
    }
    
    bool _union(int i, int j)
    {
        int parA = find(i);
        int parB = find(j);
        
        if (parA == parB)
        {
            // cant complete
            // redundent
            return false;
        }
        
        // add rank here
        if (ranks[parA] > ranks[parB])
        {
            parent[parB] = parA;
            ranks[parA] += ranks[parB];
        }
        else
        {
            parent[parA] = parB;
            ranks[parB] += ranks[parA];
        }
        
        return true;
    }
    
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        
        // init
        for (int i = 0; i < n + 1; i++)
        {
            parent.push_back(i);
            ranks.push_back(1);
        }
        
        vector<int> res;
        for (auto edge : edges)
        {
            if (!_union(edge[0], edge[1]))
            {
                res = edge;
                break;
            }
        }
        
        return res;
    }
};
```