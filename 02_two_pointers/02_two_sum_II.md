```cpp
// Problem: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        vector<int> res;
        
        while (l < r)
        {
            int sum = nums[l] + nums[r];
            if (sum == target)
            {
                res = {l + 1, r + 1};
                break;
            }
            if (sum > target)
            {
                r--;
            }
            else
            {
                l++;
            }
            
        }
        
        return res;
    }
};
```