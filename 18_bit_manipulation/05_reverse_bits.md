```cpp
// Problem: https://leetcode.com/problems/reverse-bits/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        unsigned int mask = 1, res = 0;
        
        for (int i = 0; i < 32; i++)
        {
            // shift left            
            res = res << 1;
            if (mask & n) 
                res |= 1;
            mask = mask << 1;
        }
        
        return res;
    }
};
```