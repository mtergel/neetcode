```cpp
// Problem: https://leetcode.com/problems/max-area-of-island/
// Time: O(M*N)
// Space: O(N)

class Solution {
private:
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    vector<vector<bool>> visited;

    int getArea(vector<vector<int>>& grid, int i, int j)
    {
        int area = 1;
        queue<pair<int, int>> toVisit;
        visited[i][j] = true;
        toVisit.push({i, j});

        while (!toVisit.empty())
        {
            int size = toVisit.size();
            while (size--)
            {
                auto [i, j] = toVisit.front();
                toVisit.pop();

                for (auto [x, y] : dirs)
                {
                    int ni = i + x;
                    int nj = j + y;

                    if (ni >= 0 && nj >= 0
                    &&  ni < grid.size() && nj < grid[0].size()
                    && grid[ni][nj] == 1 && !visited[ni][nj]
                    )
                    {
                        area++;
                        visited[ni][nj] = true;
                        toVisit.push({ni, nj});
                    }
                }
            }
        }

        return area;
    }

public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int res = 0;
        int m = grid.size();
        int n = grid[0].size();

        visited = vector(m, vector(n, false));

        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (grid[i][j] == 1 && !visited[i][j])
                {
                    int area = getArea(grid, i, j);
                    res = max(res, area);
                }
            }
        }

        return res;
    }
};
```