```cpp
// Problem: https://leetcode.com/problems/valid-parentheses/
// Time: O(N)
// Space: O(N)

class Solution {
public:
    bool isValid(string s) {
        if (s.size() == 1)
        {
            return false;
        }
        
        stack<char> stck;
        
        for (int i = 0; i < s.size(); i++)
        {
            char c = s[i];
            if (c == '(' || c == '{' || c == '[')
            {
                stck.push(c);
            }
            else
            {
                if (stck.empty())
                {
                    return false;
                }
                
                char prev = stck.top();
                stck.pop();
                
                if (c == ')' && prev != '(')
                {
                    return false;
                }
                if (c == '}' && prev != '{')
                {
                    return false;
                }
                if (c == ']' && prev != '[')
                {
                    return false;
                }
            }
        }
        
        return stck.empty();
    }
};
```