```cpp
// Problem: https://leetcode.com/problems/longest-palindromic-substring
// Time: O(N^2)
// Space: O(1)

class Solution {
public:
    int start;
    int maxlen;
    void checkPalindrome(const string& s, int l, int r) {
        while (l >= 0 && r < s.size() && s[l] == s[r])
        {
            l--;
            r++;
        };
        if (maxlen < r - l - 1)
        {
            maxlen = r - l - 1;
            start = l + 1;
        }
    }

    string longestPalindrome(string s) {
        int n = s.size();
        if (n < 2) return s;
        
        start = 0;
        maxlen = 0;
        
        for(int i = 0; i < n - 1; i++){
            checkPalindrome(s, i, i); // odd
            checkPalindrome(s, i, i + 1); // even
        }
        return s.substr(start, maxlen);
    }
};
```