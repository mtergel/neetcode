```cpp
// Problem: https://leetcode.com/problems/gas-station
// Time: O(N)
// Space: O(N) can be reduced to O(1)

class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        vector<int> diffs(n, 0);

        int gasSum = 0;
        int costSum = 0;

        for (int i = 0; i < n; i++)
        {
            gasSum += gas[i];
            costSum += cost[i];
            diffs[i] = gas[i] - cost[i];
        }

        if (gasSum < costSum)
        {
            return -1;
        }

        int total = 0;
        int res = 0;
        for (int i = 0; i < n; i++)
        {
            total += diffs[i];
            
            if (total < 0)
            {
                total = 0;
                res = i + 1;
            }
            
        }

        return res;
    }
};
```