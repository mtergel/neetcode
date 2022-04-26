```cpp
// Problem: https://leetcode.com/problems/rotting-oranges
// Time: O(M*N)
// Space: O(N)

class Solution {
private:
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    
public:
    int orangesRotting(vector<vector<int>>& grid) {
        // gonna assume we can modify the grid
        
        int m = grid.size();
        int n = grid[0].size();
        
        // find the starting points of the rotten oranges
        queue<pair<int, int>> rotten;
        bool hasFreshOrange = false;
        
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (hasFreshOrange == false)
                {
                    if (grid[i][j] == 1)
                    {
                        hasFreshOrange = true;
                    }
                }
                
                
                if (grid[i][j] == 2)
                {
                    rotten.push({i, j});
                }
            }
        }

        // already finished        
        if (hasFreshOrange == false)
        {
            return 0;
        }
        
        // no rotten oranges
        if (rotten.empty())
        {
            return -1;
        }
        
        
        int res = 0;
        while (!rotten.empty())
        {
            int size = rotten.size();
            while (size--)
            {
                auto [i, j] = rotten.front();
                rotten.pop();
                
                for (auto [x, y] : dirs)
                {
                    int ni = i + x;
                    int nj = j + y;
                    
                    if (ni >= 0 && nj >= 0 && ni < grid.size() && nj < grid[0].size()
                        && grid[ni][nj] == 1
                       )
                    {
                        grid[ni][nj] = 2;
                        rotten.push({ni, nj});
                    }
                }
            }
            
            res++;
        }
        
        // check if they are any fresh oranges
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (grid[i][j] == 1)
                {
                    return -1;
                }
            }
        }
        
        return res - 1;
    }
};
```