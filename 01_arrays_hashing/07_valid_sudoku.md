```cpp
// Problem: https://leetcode.com/problems/valid-sudoku/
// Time O(NM)
// Space O(1)

class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<vector<bool>> rows(9, vector(9, false));
        vector<vector<bool>> cols(9, vector(9, false));
        vector<vector<vector<bool>>> blocks(3, vector(3, vector(9, false)));
        
        for (int i = 0; i < board.size(); i++)
        {
            for (int j = 0; j < board[0].size(); j++)
            {
                if (board[i][j] == '.')
                {
                    continue;
                }
                int num = board[i][j] - '1';
                
                // check row
                if (rows[i][num])
                {
                    return false;
                }
                else
                {
                    rows[i][num] = true;
                }
                
                // check col
                if (cols[num][j])
                {
                    return false;
                }
                else
                {
                    cols[num][j] = true;
                }
                
                // check block
                if (blocks[i / 3][j / 3][num])
                {
                    return false;
                }
                else
                {
                    blocks[i / 3][j / 3][num] = true;
                }
                
                
            }
        }
        
        return true;
    }
};
```