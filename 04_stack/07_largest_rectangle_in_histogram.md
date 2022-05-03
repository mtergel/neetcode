```cpp
// Problem: https://leetcode.com/problems/trapping-rain-water
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> mono;
        int area = 0;
        
        // adding stopping point
        // to clear monotonic stack
        heights.push_back(0);
        
        for (int i = 0; i < heights.size(); i++)
        {
            while (!mono.empty() && heights[mono.top()] >= heights[i])
            {
                int maxHeightPossible = heights[mono.top()];
                mono.pop();
                
                int l = mono.empty() ? -1 : mono.top();
                
                // i - l - 1
                // r - l - 1 width
                // not including the current ith bar
                // since it is lower than
                // the candidate
                
                area = max(area, maxHeightPossible * (i - l - 1));
            }
            mono.push(i);
        }
        
        return area;
    }
};
```