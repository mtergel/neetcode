```cpp
// Problem: https://leetcode.com/problems/rotting-oranges
// Time: O(M*N)
// Space: O(N)

class Solution {
private: 
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
public:
    /**
     * @param rooms: m x n 2D grid
     * @return: nothing
     */
    void wallsAndGates(vector<vector<int>> &rooms) {
        // find gates?
        // start bfs from the gates
        // skip walls
        // update values of rooms with min value

        int m = rooms.size();
        int n = rooms[0].size();

        queue<pair<int, int>> toVisit;
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (rooms[i][j] == 0)
                {
                    toVisit.push({i, j});
                }
            }
        }

        if (toVisit.empty())
        {
            return;
        }

        int distance = 1;
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

                    if (ni >= 0 && nj >= 0 && ni < m && nj < n
                    && rooms[ni][nj] == INT_MAX
                    )
                    {
                        rooms[ni][nj] = distance;
                        toVisit.push({ni, nj});
                    }
                }
            }

            distance++;
        }

        return;
    }
};
```