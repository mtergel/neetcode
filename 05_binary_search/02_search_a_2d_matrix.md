```cpp
// Problem: https://leetcode.com/problems/search-a-2d-matrix/
// Time: O(logMN)
// Space: O(1)

class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();
        
        int l = 0, r = (m * n) - 1;
        
        while (l <= r)
        {
            int mid = l + (r - l) / 2;
            int ele = matrix[mid / n][mid % n];
            
            if (ele == target)
            {
                return true;
            }
            
            if (ele > target)
            {
                r = mid - 1;
            }
            else
            {
                l = mid + 1;
            }
        }
        
        return false;
    }
};
```