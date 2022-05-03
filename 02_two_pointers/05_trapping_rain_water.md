```cpp
// Problem: https://leetcode.com/problems/trapping-rain-water
// Time: O(N)
// Space: O(1)

class Solution {
public:
    int trap(vector<int>& height) {
        if (height.size() < 3)
        {
            return 0;
        }
        
        int l = 0, r = height.size() - 1;
        
        int maxLeft = height[l];
        int maxRight = height[r];
        int res = 0;
        
        while (l < r)
        {
            // finding the bottleneck
            if (maxLeft < maxRight)
            {
                l++;
                maxLeft = max(maxLeft, height[l]);
                res += maxLeft - height[l];
            }
            else
            {
                r--;
                maxRight = max(maxRight, height[r]);
                res += maxRight - height[r];
            }
        }
        
        return res;
    }
};
```