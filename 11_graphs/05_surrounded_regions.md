```cpp
// Problem: https://leetcode.com/problems/surrounded-regions/
// Time: O(M*N)
// Space: O(N)

class Solution {
private:
    const int dirs[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    
    vector<vector<bool>> safe;
    void markSafe(vector<vector<char>>& board, int i, int j) 
    {
        safe[i][j] = true;
        queue<pair<int, int>> q;
        q.push({i, j});
        
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
                    
                    if (ni >= 0 && nj >= 0 && ni < board.size() && nj < board[0].size()
                    && board[ni][nj] == 'O' && !safe[ni][nj]
                       )
                    {
                        safe[ni][nj] = true;
                        q.push({ni, nj});
                    }
                }
            }
        }
    }
    
public:
    void solve(vector<vector<char>>& board) {
        // mark 'O's that are connected to the board
        int m = board.size();
        int n = board[0].size();
        
        safe = vector(m, vector(n, false));
        
        for (int i = 0; i < m; i++)
        {
            // left
            if (board[i][0] == 'O' && !safe[i][0])
            {
                markSafe(board, i, 0);
            }
            
            if (board[i][n - 1] == 'O' && !safe[i][n - 1])
            {
                markSafe(board, i, n - 1);
            }
        }
        
        for (int j = 0; j < n; j++)
        {
            // up
            if (board[0][j] == 'O' && !safe[0][j])
            {
                markSafe(board, 0, j);
            }
            
            // down
            if (board[m - 1][j] == 'O' && !safe[m - 1][j])
            {
                markSafe(board, m - 1, j);
            }
        }
        
        // remove every non safe 'O'
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (board[i][j] == 'O' && !safe[i][j])
                {
                    board[i][j] = 'X';
                }
            }
        }
        
        return;
    }
};
```