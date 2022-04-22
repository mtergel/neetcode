```cpp
// Problem: https://leetcode.com/problems/evaluate-reverse-polish-notation
// Time: O(N)
// Space: O(N)

class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> nums;
        for (const string &token : tokens)
        {
            if (token == "+" || token == "-" || token == "*" || token == "/")
            {
                
                // pop the last 2 nums

                int operand2 = nums.top();
                nums.pop();

                int operand1 = nums.top();
                nums.pop();
                
                switch(token[0])
                {
                    case '+': 
                        nums.push(operand1 + operand2);
                        break;
                    case '-':
                        nums.push(operand1 - operand2);
                        break;
                    case '*':
                        nums.push(operand1 * operand2);
                        break;
                    case '/':
                        nums.push(operand1 / operand2);
                        break;
                }
            }
            else
            {
                nums.push(atoi(token.c_str()));
            }
        }
        
        return nums.top();
    }
};
```