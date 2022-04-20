```cpp
// Problem: https://leetcode.com/problems/min-stack/
// Time: O(N) N - number of actions
// Space: O(K) K - number of push actions

// This solution uses two stacks
// Or can use stack of pair<int, int>
// number, current min_number;
class MinStack {
public:
    stack<int> minStack;
    stack<int> normStack;
    MinStack() {
        
    }
    
    void push(int val) {
        normStack.push(val);
        if (minStack.empty() || val <= minStack.top())
        {
            minStack.push(val);
        }
    }
    
    void pop() {
        if (normStack.top() == minStack.top())
        {
            minStack.pop();
        }
        
        normStack.pop();
    }
    
    int top() {
        return normStack.top();
    }
    
    int getMin() {
        return minStack.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```