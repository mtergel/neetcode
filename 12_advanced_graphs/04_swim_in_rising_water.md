```cpp
// Problem: https://leetcode.com/problems/swim-in-rising-water
// Time: O(N^2 * logn)
// Space: O(N^2)

typedef pair<int, pair<int, int>> timenode;
class Solution {
private:
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    
public:
    int swimInWater(vector<vector<int>>& grid) {
        int n = grid.size();
        if (n == 1)
        {
            return 0;
        }
        
        vector<vector<bool>> visited(n, vector(n, false));
        priority_queue<timenode, vector<timenode>, greater<timenode>> pq;
        
        pq.push({grid[0][0], {0, 0}});
        visited[0][0] = true;
        
        while (!pq.empty())
        {
            auto [time, coords] = pq.top();
            pq.pop();
            
            if (coords.first == n - 1 && coords.second == n - 1)
            {
                return time;
            }
            
            for (auto [x, y] : dirs)
            {
                int ni = coords.first + x;
                int nj = coords.second + y;
                
                if (ni >= 0 && nj >= 0 && ni < n && nj < n && !visited[ni][nj])
                {
                    visited[ni][nj] = true;
                    pq.push({max(time, grid[ni][nj]), {ni, nj}});
                }
            }
        }
        
        return -1;
    }
};
```