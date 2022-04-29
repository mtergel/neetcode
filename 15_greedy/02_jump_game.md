```cpp
// Problem: https://leetcode.com/problems/jump-game/
// Time: O(N)
// Space: O(1)

class Solution {
public:
    bool canJump(vector<int>& nums) {
        int goal = nums.size() - 1;

        // 2, 3, 1, 1, 4
        for (int i = goal - 1; i >= 0; i--)
        {
            if (nums[i] + i >= goal)
            {
                goal = i;
            }
        }

        return goal == 0;
    }
};
```