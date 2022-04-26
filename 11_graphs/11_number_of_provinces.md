```cpp
// Problem: https://leetcode.com/problems/number-of-provinces
// Time: ~O(N)
// Space: O(N)

class Solution {
private:
    vector<int> parents;
    vector<int> ranks;
    
    int find(int n)
    {
        if (parents[n] == n)
        {
            return n;
        }
        
        parents[n] = find(parents[n]);
        return parents[n];
    }
    
    void _union(int i, int j)
    {
        int parA = parents[i];
        int parB = parents[j];
        
        if (parA == parB)
        {
            return;
        }
        
        if (ranks[parA] > ranks[parB])
        {
            parents[parB] = parA;
            ranks[parA] += ranks[parB];
        }
        else
        {
            parents[parA] = parB;
            ranks[parB] += ranks[parA];
        }
    }
    
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        for (int i = 0; i < n; i++)
        {
            // everyone is parent of themselves
            parents.push_back(i);
            ranks.push_back(1);
        }
        
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (isConnected[i][j])
                {
                    _union(i, j);                    
                }
            }
        }
        
        int res = 0;
        for (int i = 0; i < n; i++)
        {
            if (parents[i] == i)
            {
                res++;
            }
        }
            
        return res;
    }
};
```