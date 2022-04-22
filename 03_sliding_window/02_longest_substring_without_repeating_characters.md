```cpp
// Problem: https://leetcode.com/problems/longest-substring-without-repeating-characters/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() == 0 || s.size() == 1)
        {
            return s.size();
        }
        
        unordered_set<char> seen;
        
        int l = 0, r = 0, n = s.size();
        int res = 1;
        
        while (r < n)
        {
            if (seen.empty() || seen.find(s[r]) == seen.end())
            {
                seen.insert(s[r]);
                res = max(res, r - l + 1);
            }
            else
            {
                while(l < r && s[l] != s[r])
                {
                    seen.erase(s[l]);
                    l++;
                }
                l++;
            }
            
            r++;
        }
        
        return res;
    }
};
```