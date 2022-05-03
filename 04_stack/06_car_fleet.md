```cpp
// Problem: https://leetcode.com/problems/car-fleet/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int carFleet(int target, vector<int>& position, vector<int>& speed) {
        if (position.empty() || speed.empty()) return 0;
        
        int n = position.size();
        vector<pair<int, double>> intervals; // start position, arrival time
        for (int i = 0; i < position.size(); i++)
        intervals.push_back(make_pair(position[i], (double)(target - position[i])/(double)(speed[i])));
        sort(intervals.begin(), intervals.end());

        int res = 1; 
        pair<int,double> curr;
        curr = intervals[intervals.size() - 1];

        for (int i = intervals.size() - 2; i >= 0; i--) {
            if (intervals[i].second > curr.second) {
                res++;
                curr = intervals[i];
            }
        }	
        return res;
    }
};
```