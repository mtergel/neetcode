```cpp
// Problem: https://leetcode.com/problems/counting-bits/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> res(n+1, 0);
        for (int i = 1; i <= n; i++) {
            res[i] = res[i & (i - 1)] + 1;
        }
        return res;
    }
};
```