```cpp
// Problem: https://leetcode.com/problems/spiral-matrix
// Time: O(N)
// Space: O(1)

class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        
        int l = 0, t = 0;
        int r = n - 1, b = m - 1;
        
        vector<int> res;
        while (l <= r && t <= b)
        {
            for (int j = l; j <= r; j++)
            {
                res.push_back(matrix[t][j]);
            }
            
            t++;
            
            for (int i = t; i <= b; i++)
            {
                res.push_back(matrix[i][r]);
            }
            
            r--;
            
            if (t <= b)
            {
                for (int j = r; j >= l; j--)
                {
                    res.push_back(matrix[b][j]);
                }
            }
            
            b--;
            
            if (l <= r)
            {
                for (int i = b; i >= t; i--)
                {
                    res.push_back(matrix[i][l]);
                }
            }
            
            l++;
        }
        
        return res;
    }
};
```