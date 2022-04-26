```cpp
// Problem: https://leetcode.com/problems/number-of-1-bits/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res = 0;
        
        // will loop for every 1 bit in n
        // not every bit in n
        while (n > 0)
        {
            // drops the lowest set bit e.g
            // lowest 1 bit
            n = n & n - 1;
            res++;
        }
        
        return res;
    }
};
```