```cpp
// Problem: https://leetcode.com/problems/last-stone-weight/
// Time: O(N * logN)
// Space: O(N)

class Solution {
public:
    int lastStoneWeight(vector<int>& stones) {
        
        if (stones.size() < 2)
        {
            return stones[0];
        }
        
        priority_queue<int> maxheap;
        for (int stone : stones)
        {
            maxheap.push(stone);
        }
        
        int y;
        int x;
        
        while (maxheap.size() > 1)
        {
            y = maxheap.top();
            maxheap.pop();
            
            x = maxheap.top();
            maxheap.pop();
            
            if (x < y)
            {
                maxheap.push(y - x);
            }
        }
        
        return maxheap.size() == 0 ? 0 : maxheap.top();
    }
};
```