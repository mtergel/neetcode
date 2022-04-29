```cpp
// Problem: https://leetcode.com/problems/jump-game-ii/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    int jump(vector<int>& nums) {
        int n = nums.size();
        if (n == 1)
        {
            return 0;
        }
        
        int res = 0;
        int l = 0, r = 0;
        
        while (r < n - 1)
        {
            int far = 0;
            for (int i = l; i <= r; i++)
            {
                far = max(far, i + nums[i]);
            }
            
            l = r + 1;
            r = far;
            res++;
        }
        
        return res;
    }
};
```