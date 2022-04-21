```cpp
// Problem: https://leetcode.com/problems/maximum-subarray/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = nums[0];
        int curr = nums[0];
        
        for (int i = 1; i < nums.size(); i++)
        {
            curr = max(nums[i], curr + nums[i]);
            res = max(res, curr);
        }
        
        return res;
    }
};
```