```cpp
// Problem: https://leetcode.com/problems/happy-number
// Time: O(N)
// Space: O(1)

class Solution {
private:
    int getNext(int curr)
    {
        int sum = 0;
        while (curr)
        {
            int digit = curr % 10;
            sum += digit * digit;
            curr /= 10;
        }
        
        return sum;
        
    }
public:
    bool isHappy(int n) {
        int slow = n;
        int fast = n;
        
        do
        {
            slow = getNext(slow);
            fast = getNext(getNext(fast));
        }
        while (slow != fast);
        
        
        return slow == 1;
        
    }
};
```