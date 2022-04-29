```cpp
// Problem: https://leetcode.com/problems/insert-interval
// Time: O(N)
// Space: O(1)

class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int n = intervals.size();
        vector<vector<int>> res;
        
        if (n == 0)
        {
            res.push_back(newInterval);
            return res;
        }
        
        // find the insert point
        int start = 0;
        while (start < n && intervals[start][1] < newInterval[0])
        {
            res.push_back(intervals[start]);
            start++;
        }
        
        // and merge the remaining intervals
        while (start < n && intervals[start][0] <= newInterval[1])
        {
            newInterval[0] = min(newInterval[0], intervals[start][0]);
            newInterval[1] = max(newInterval[1], intervals[start][1]);
            start++;
        }
        
        res.push_back(newInterval);
        
        // push the rest of the intervals
        while (start < n)
        {
            res.push_back(intervals[start]);
            start++;
        }
        
        return res;
    }
};
```