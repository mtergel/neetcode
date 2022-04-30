```cpp
// Problem: https://leetcode.com/problems/powx-n/
// Time: O(logn)
// Space: O(1)

class Solution {
public:
    double myPow(double x, int n) {
        // 2^10 = 2^5 * 2^5
        // 2^5 = 2^2 * 2^2 * 2
        // 2^2 = 2^1 * 2^1

        if (n == 0 || x == 1)
        {
            return 1;
        }

        if (n < 0)
        {
            n = abs(n);
            x = 1 / x;
        }
        
        if (n % 2 == 0)
        {
            return myPow(x * x, n / 2);
        }
        else
        {
            return x * myPow(x * x, n / 2);
        }
    }
};
```