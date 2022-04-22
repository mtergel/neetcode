```cpp
// Problem: https://leetcode.com/problems/evaluate-reverse-polish-notation
// Time: O(N)
// Space: O(N)

class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temp) {
        
        // monotonic stack
        stack<int> mono;
        vector<int> res(temp.size(), 0);
        
        for (int i = 0; i < temp.size(); i++)
        {
            while (!mono.empty() && temp[i] > temp[mono.top()])
            {
                int prev = mono.top();
                res[prev] = i - prev;
                mono.pop();
            }
            
            mono.push(i);
            
        }
        
        return res;
        
    }
};
```