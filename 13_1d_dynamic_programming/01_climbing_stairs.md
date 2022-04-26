```cpp
// Problem: https://leetcode.com/problems/climbing-stairs/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    int climbStairs(int n) {
        if (n == 1)
        {
            return 1;
        }
        
        if (n == 2)
        {
            return 2;
        }
        
        int prev1 = 1;
        int prev2 = 2;
        
        for (int i = 2; i < n; i++)
        {
            int tmp = prev2;
            prev2 = prev1 + prev2;
            prev1 = tmp;
        }
        
        return prev2;
    }
};
```