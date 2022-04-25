```cpp
// Problem: https://leetcode.com/problems/palindrome-partitioning/
// Time: O(N*2^N)
// Space: O(N * N)

class Solution {
private:
    vector<vector<string>> res;
    void helper(string& s, vector<string>& path, int start)
    {
        if (start >= s.size())
        {
            res.push_back(path);
            return;
        }
        
        for (int end = start; end < s.size(); end++)
        {
            if (isPalindrome(s, start, end))
            {
                path.push_back(s.substr(start, end - start + 1));
                helper(s, path, end + 1);
                path.pop_back();                
            }
        }
    }
    
    bool isPalindrome(string& s, int low, int high)
    {
        while (low < high)
        {
            if (s[low] != s[high])
            {
                return false;
            }
            
            low++;
            high--;
        }
        
        return true;
    }
    
public:
    vector<vector<string>> partition(string s) {
        vector<string> path;
        
        helper(s, path, 0);
        
        return res;
    }
};
```