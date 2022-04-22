```cpp
// Problem: https://leetcode.com/problems/evaluate-reverse-polish-notation
// Time: O(N)-th Catalan number
// Space: O(N)-th Catalan number

class Solution {
private:
    vector<string> res;
    void backtrack(string &curr, int open, int close, int max)
    {
        if (curr.size() == max * 2)
        {
            res.push_back(curr);
            return;
        }
        
        if (open < max)
        {
            // add open
            curr += '(';
            backtrack(curr, open + 1, close, max);
            curr.pop_back();
        }
        
        if (close < open)
        {
            curr += ')';
            backtrack(curr, open, close + 1, max);
            curr.pop_back();
        }
    }
    
    
public:
    vector<string> generateParenthesis(int n) {
        string path;
        backtrack(path, 0, 0, n);
        
        return res;
    }
};
```