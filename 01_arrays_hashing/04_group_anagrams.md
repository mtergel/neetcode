```cpp
// Problem: https://leetcode.com/problems/group-anagrams/
// Time O(N)
// Space O(N)

class Solution {
private:
    string countingSort(string s) {
        int counter[26] = {0};
        for (char c : s)
        {
            counter[c - 'a']++;
        }
        
        string t;
        for (int i = 0; i < 26; i++)
        {
            t += string(counter[i], i + 'a');
        }
        
        return t;
    };
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        int n = strs.size();
        unordered_map<string, vector<string>> dict;
        
        for (const auto& str : strs) // O(N)
        {
            string t = countingSort(str); // O(N)
            
            dict[t].push_back(str);
        }
        
        res.reserve(dict.size());
        for (auto it = dict.begin(); it != dict.end(); it++)
        {
            res.push_back(move(it->second));
        }
        
        return res;
    }
};
```