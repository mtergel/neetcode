```cpp
// Problem: https://leetcode.com/problems/rotting-oranges
// Time: O(N)
// Space: O(N)

class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        vector<int> indegree(numCourses);
        
        // build graph into adj list
        for (auto p : prerequisites)
        {
            // directed
            // since its an prerequisite
            
            // add connection
            adj[p[1]].push_back(p[0]);
            
            // increase its indegree count
            indegree[p[0]]++;
        }
        
        int count = numCourses;
        queue<int> s;
        
        for (int i = 0; i < numCourses; i++)
        {
            if (indegree[i] == 0)
            {
                s.push(i);
            }
        }
        
        while (!s.empty())
        {
            int curr = s.front();
            s.pop();
            count--;
            
            for (int neigh : adj[curr])
            {
                indegree[neigh]--;
                
                if (indegree[neigh] == 0)
                {
                    s.push(neigh);
                }
            }
        }
        
        return count == 0;
    }
};
```