```cpp
// Problem: https://leetcode.com/problems/valid-parenthesis-string/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    bool checkValidString(string s) {
        int leftMax = 0; // when * becomes (
        int leftMin = 0; // when * becomes ) if it becomes - reset it back 0 since we can also skip it

        for (int i = 0; i < s.size(); i++)
        {
            if (s[i] == '(')
            {
                leftMin++;
                leftMax++;
            }
            else if (s[i] == ')')
            {
                leftMin--;
                leftMax--;
            }
            else
            {
                leftMin--;
                leftMax++;
            }

            if (leftMax < 0)
            {
                return false;
            }

            // ( * )
            leftMin = max(leftMin, 0);
        }

        return leftMin == 0;
    }
}; 
```