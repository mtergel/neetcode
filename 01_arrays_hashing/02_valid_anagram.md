```cpp
// Problem: https://leetcode.com/problems/valid-anagram/
// Time: O(N)
// Space: O(26)
// Follow up: Use a hash map i guess

class Solution {
public:
    bool isAnagram(string s, string t) {
        // since it only consist of lowercase English letters
        // can use 26 length vector to count the letters
        
        vector<int> sLetters(26, 0);
        vector<int> tLetters(26, 0);
        
        if (s.size() != t.size())
        {
            return false;
        }
        
        for (int i = 0; i < s.size(); i++)
        {
            sLetters[s[i] - 'a']++;
            tLetters[t[i] - 'a']++;
        }
        
        for (int i = 0; i < 26; i++)
        {
            if (sLetters[i] != tLetters[i])
            {
                return false;
            }
        }
        
        return true;
    }
};
```