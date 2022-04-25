```cpp
// Problem: https://leetcode.com/problems/letter-combinations-of-a-phone-number
// Time: O(N*2^N)
// Space: O(N * N)
class Solution {
private:
    const vector<string> letters = {
        "", "", "abc", "def", "ghi", "jkl",
        "mno", "pqrs", "tuv", "wxyz"
    };
    
    vector<string> res;
    
    void helper(string& digits, int start, string& path)
    {
        if (start == digits.size())
        {
            res.push_back(path);
            return;
        }
        
        for (auto c : letters[digits[start] - '0'])
        {
            path.push_back(c);
            helper(digits, start + 1, path);
            path.pop_back();
        }
    }
    
public:
    vector<string> letterCombinations(string digits) {
        
        if (digits.empty())
        {
            return res;
        }
        
        string path;
        helper(digits, 0, path);
        
        return res;
    }
};
```