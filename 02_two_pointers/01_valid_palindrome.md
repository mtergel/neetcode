```cpp
// Problem: https://leetcode.com/problems/valid-palindrome/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    bool isPalindrome(string s) {
        int l = 0, r = s.size() - 1;
        while (l < r)
        {
            // move l
            while (l < r && !isalnum(s[l]))
            {
                l++;
            }
            
            // move r
            while (l < r && !isalnum(s[r]))
            {
                r--;
            }
            
            if (tolower(s[l]) != tolower(s[r]))
            {
                return false;
            }
            
            l++;
            r--;
        }
        
        return true;
    }
};
```