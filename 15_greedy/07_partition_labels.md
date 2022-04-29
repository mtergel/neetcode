```cpp
// Problem: https://leetcode.com/problems/partition-labels/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    vector<int> partitionLabels(string s) {
        vector<int> res;
        int n = s.size();
        unordered_map<char, int> lastIndex;
        
        for (int i = 0; i < n; i++)
        {
            lastIndex[s[i]] = i;
        }            

        int size = 0;
        int end = 0;
        
        for (int i = 0; i < n; i++)
        {
            size++;
            end = max(end, lastIndex[s[i]]);
            
            if (i == end)
            {
                res.push_back(size);
                size = 0;
            }
        }
        
        return res;
    }
};
```