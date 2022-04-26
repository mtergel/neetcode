```cpp
// Problem: https://leetcode.com/problems/rotting-oranges
// Time: O(N + E)
// Space: O(N + E)

class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        vector<int> indegree(numCourses);
        
        for (auto p : prerequisites)
        {
            adj[p[1]].push_back(p[0]);
            indegree[p[0]]++;
        }
        
        queue<int> s;
        for (int i = 0; i < numCourses; i++)
        {
            if (indegree[i] == 0)
            {
                s.push(i);
            }
        }
        
        int count = numCourses;
        vector<int> res;
        
        while (!s.empty())
        {
            int curr = s.front();
            s.pop();
            count--;
            res.push_back(curr);
            
            for (auto neigh : adj[curr])
            {
                indegree[neigh]--;
                
                if (indegree[neigh] == 0)
                {
                    s.push(neigh);
                }
            }
        }
        
        if (count == 0)
        {
            return res;
        }
        else
        {
            return {};
        }
    }
};
```