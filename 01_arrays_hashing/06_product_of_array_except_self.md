```cpp
// Problem: https://leetcode.com/problems/product-of-array-except-self
// Time O(N)
// Space O(N)

class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> res(n, 1);
        
        // prefix
        for (int i = 1; i < n; i++)
        {
            res[i] = res[i - 1] * nums[i - 1];
        }
        
        // suffix
        int suffixSum = 1;
        for (int i = n - 1; i >= 0; i--)
        {
            res[i] = suffixSum * res[i];
            suffixSum *= nums[i];
        }
        
        return res;
    }
};
```