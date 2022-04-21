```cpp
// Problem: https://leetcode.com/problems/longest-consecutive-sequence
// Time O(N)
// Space O(N)

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        if (n == 0 || n == 1)
        {
            return n;
        }
        
        set<int> seen;
        for (int num : nums)
        {
            seen.insert(num);
        }
        
        int maxLCS = 1;
        int currentMax = 1;
        
        for (auto it = seen.begin(); it != seen.end(); it++)
        {
            int num = *it;
            if (seen.find(num + 1) != seen.end())
            {
                currentMax++;
                maxLCS = max(maxLCS, currentMax);
            }
            else
            {
                currentMax = 1;
            }
        }
        
        return maxLCS;
        
    }
};
```