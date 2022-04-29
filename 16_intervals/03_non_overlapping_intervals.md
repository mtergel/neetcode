```cpp
// Problem: https://leetcode.com/problems/non-overlapping-intervals/
// Time: O(nlogn)
// Space: O(N)

class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        int res = 0;
        sort(intervals.begin(), intervals.end(), [](const vector<int>& lhs, const vector<int>& rhs) -> bool {
            return lhs[0] < rhs[0];
        });

        int curr = intervals[0][1];
        for (int i = 1; i < intervals.size(); i++)
        {
            if (intervals[i][0] < curr)
            {
                res++;
                curr = min(curr, intervals[i][1]);
            }
            else
            {
                curr = intervals[i][1];
            }
        }

        return res;
    }
};
```