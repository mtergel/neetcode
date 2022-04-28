```cpp
// Problem: https://leetcode.com/problems/longest-palindromic-substring
// Time: O(N^2)
// Space: O(1)

class Solution {
private:
    int countSS(int l, int r, const string& s)
    {
        int res = 0;
        while (l >= 0 && r < s.size() && s[l] == s[r])
        {
            res++;
            l--;
            r++;
        }
        
        return res;
    }
public:
    int countSubstrings(string s) {
        int count = 0;
        for (int i = 0; i < s.size(); i++)
        {
            count += countSS(i, i, s);
            count += countSS(i, i + 1, s);
        }
        
        return count;
    }
};
```