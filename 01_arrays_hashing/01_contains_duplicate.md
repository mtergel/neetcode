```cpp
// Problem: https://leetcode.com/problems/contains-duplicate/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> seen;
        for (int num : nums)
        {
            if (seen.find(num) == seen.end())
            {
                seen.insert(num);
            }
            else
            {
                return true;
            }
        }
        
        return false;
    }
};
```