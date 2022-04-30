```cpp
// Problem: https://leetcode.com/problems/set-matrix-zeroes
// Time: O(NN)
// Space: O(1)

class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        
        // mark if the first col has 0
        bool isCol = false;
        
        // we are gonna mark the first cell of each col/row 0
        
        for (int i = 0; i < m; i++)
        {
            // check first col
            if (matrix[i][0] == 0)
            {
                isCol = true;
            }
            
            // check the rest of the grid
            for (int j = 1; j < n; j++)
            {
                if (matrix[i][j] == 0)
                {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        
        // set grid to 0        
        for (int i = 1; i < m; i++)
        {
            for (int j = 1; j < n; j++)
            {
                if (matrix[i][0] == 0 || matrix[0][j] == 0)
                {
                    matrix[i][j] = 0;
                }
            }
        }
        
        // check if top row has any 0
        if (matrix[0][0] == 0)
        {
            for (int j = 0; j < n; j++)
            {
                matrix[0][j] = 0;
            }
        }
        
        // check if first col has any 0
        if (isCol)
        {
            for (int i = 0; i < m; i++)
            {
                matrix[i][0] = 0;
            }
        }
    }
};
```