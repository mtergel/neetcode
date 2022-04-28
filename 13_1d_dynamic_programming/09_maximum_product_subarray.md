```cpp
// Problem: https://leetcode.com/problems/maximum-product-subarray
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();
        if (n == 1)
        {
            return nums[0];
        }
        
        int minusMax = nums[0];
        int plusMax = nums[0];
        
        int res = nums[0];
        for (int i = 1; i < n; i++)
        {
            int tmp = min(nums[i], nums[i] * (nums[i] >= 0 ? minusMax : plusMax));
            plusMax = max(nums[i], nums[i] * (nums[i] >= 0 ? plusMax : minusMax));
            minusMax = tmp;
            
            res = max(res, plusMax);
        }
        
        
        return res;
    }
};
```