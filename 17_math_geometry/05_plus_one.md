```cpp
// Problem: https://leetcode.com/problems/plus-one/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size() - 1;
        
        for (int i = n; i >= 0; i--)
        {
            if (digits[i] == 9)
            {
                digits[i] = 0;
            }
            else
            {
                digits[i]++;
                return digits;
            }
        }
        
        // if get to the most significant digit
        // and we have carry remaining
        digits.push_back(0);
        digits[0] = 1;
        return digits;
    }
};
```