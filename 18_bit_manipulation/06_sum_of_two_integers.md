```cpp
// Problem: https://leetcode.com/problems/sum-of-two-integers/
// Time: O(1)
// Space: O(1)

class Solution {
public:
    int getSum(int a, int b) {
        
        // xor of a + b (sum without carry)
        // +
        // and of a + b (sum of carry)
        
        
        if (b == 0)
        {
            return a;
        }
        
        return getSum(a^b, (unsigned int)(a & b) << 1);
    }
};
```