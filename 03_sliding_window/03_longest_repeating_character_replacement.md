```cpp
// Problem: https://leetcode.com/problems/longest-repeating-character-replacement/
// Time: O(N)
// Space: O(26)

class Solution {
public:
    int characterReplacement(string s, int k) {
        int n = s.size();
        if (n == 0 || n == 1 || n == k)
        {
            return n;
        }
        
        int l = 0, r = 0;
        int res = 0;
        int maxCount = 0;
        
        vector<int> count(26, 0);
        
        while (r < n)
        {
            // grow window
            count[s[r] - 'A']++;
            
            // this character could be
            // the longest repeating character
            maxCount = max(maxCount, count[s[r] -'A']);
            
            // shrink window
            while (r - l + 1 - maxCount > k)
            {
                count[s[l] - 'A']--;
                l++;
            }
            
            res = max(res, r - l + 1);
            
            r++;
        }
        
        return res;
    }
};
```