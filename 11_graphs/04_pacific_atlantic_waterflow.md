```cpp
// Problem: https://leetcode.com/problems/max-area-of-island/
// Time: O(M*N)
// Space: O(N)

class Solution {
private:
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    void markVisited (vector<vector<bool>>& visited, vector<vector<int>>& heights,  int i, int j) {
        
        visited[i][j] = true;
        int prevHeight = heights[i][j];

        for (auto [x, y] : dirs)
        {
            int ni = i + x;
            int nj = j + y;

            if (ni >= 0 && nj >= 0 && ni < heights.size() && nj < heights[0].size()
            && heights[ni][nj] >= prevHeight && !visited[ni][nj]
            )
            {
                markVisited(visited, heights, ni, nj);
            }
        }
    }


public:
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        int m = heights.size();
        int n = heights[0].size();

        vector<vector<bool>> pVisited(m, vector(n, false));
        vector<vector<bool>> aVisited(m, vector(n, false));

        for (int i = 0; i < m; i++)
        {
            // left
            markVisited(pVisited, heights, i, 0);

            // right
            markVisited(aVisited, heights, i, n - 1);
        }

        for (int j = 0; j < n; j++)
        {
            // up
            markVisited(pVisited, heights, 0, j);

            // down
            markVisited(aVisited, heights, m - 1, j);
        }


        vector<vector<int>> res;

        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (pVisited[i][j] && aVisited[i][j])
                {
                    res.push_back({i, j});
                }
            }
        }


        return res;
    }
};
```