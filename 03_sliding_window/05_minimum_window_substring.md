```cpp
// Problem: https://leetcode.com/problems/permutation-in-string/
// Time: O(S + T)
// Space: O(52?)

class Solution {
public:
    string minWindow(string s, string t) {
        if (t.size() > s.size())
        {
            return "";
        }
        
        unordered_map<char, int> tCount, window;
        
        for (int i = 0; i < t.size(); i++)
        {
            tCount[t[i]]++;
        }
        
        int shouldBe = tCount.size();
        int matches = 0;
        int l = 0;
        
        string res = "";
        int resLength = INT_MAX;
        
        // sliding window
        for (int r = 0; r < s.size(); r++)
        {
            // grow the window
            window[s[r]]++;
            
            if (tCount.find(s[r]) != tCount.end()
               && tCount[s[r]] == window[s[r]]
               )
            {
                matches++;
            }
            
            // try to shrink the window
            while (matches == shouldBe)
            {
                if (r - l + 1 < resLength)
                {
                    resLength = r - l + 1;
                    res = s.substr(l, resLength);
                }
                
                window[s[l]]--;
                
                if (tCount.find(s[l]) != tCount.end() && window[s[l]] < tCount[s[l]])
                {
                    matches--;
                }
                
                l++;
            }
        }
        
        return resLength == INT_MAX ? "" : res;
    }
};
```