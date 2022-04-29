```cpp
// Problem: https://leetcode.com/problems/merge-intervals/
// Time: O(nlogn)
// Space: O(N)

class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> res;

        sort(intervals.begin(), intervals.end(), [](const vector<int>& lhs, const vector<int>& rhs) -> bool {
            return lhs[0] < rhs[0];
        });

       for (vector<int> interval : intervals)
       {
           if (res.empty() || res.back()[1] < interval[0])
           {
               res.push_back(interval);
           }
           else
           {
               res.back()[1] = max(res.back()[1], interval[1]);
           }
       }

        return res;
    }
};
```