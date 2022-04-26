```cpp
// Problem: https://leetcode.com/problems/number-of-islands/
// Time: O(M * N)
// Space: O(N)

class Solution {
private:
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    vector<vector<bool>> visited;

    void markIsland(vector<vector<char>>& grid, int i, int j)
    {
        queue<pair<int, int>> q;
        q.push({i, j});
        visited[i][j] = true;

        while (!q.empty())
        {
            int size = q.size();
            while (size--)
            {
                auto [i, j] = q.front();
                q.pop();
                
                for (auto [x, y] : dirs)
                {
                    int ni = i + x;
                    int nj = j + y;

                    if (ni >= 0 && nj >= 0
                     && ni < grid.size() && nj < grid[0].size()
                    && grid[ni][nj] == '1' && !visited[ni][nj]
                     )
                     {
                         visited[ni][nj] = true;
                         q.push({ni, nj});
                     }
                }

            }
        }
    }

public:
    int numIslands(vector<vector<char>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        visited = vector(m, vector(n, false));
        
        int res = 0;

        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (grid[i][j] == '1' && !visited[i][j])
                {
                    res++;
                    markIsland(grid, i, j);
                }
            }
        }

        return res;
    }
};
```