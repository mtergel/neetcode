```cpp
// Problem: https://leetcode.com/problems/single-number/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = nums[0];
        
        for (int i = 1; i < nums.size(); i++)
        {
            res ^= nums[i];
        }
        
        return res;
    }
};
```