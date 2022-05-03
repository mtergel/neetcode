```cpp
// Problem: https://leetcode.com/problems/permutation-in-string/
// Time: O(N)
// Space: O(K)

class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> buffer;
        vector<int> res;
        
        // buffer will maintain
        // monotonically decreasing queue
        
        int n = nums.size();
        for (int i = 0; i < n; i++)
        {
            // edge case when
            // the largest element
            // is in the previous windows front
            
            if (!buffer.empty() && buffer.front() == i - k)
            {
                buffer.pop_front();
            }
            
            while (!buffer.empty() && nums[buffer.back()] < nums[i])
            {
                buffer.pop_back();
            }
            
            buffer.push_back(i);
            
            
            if (i - k + 1 >= 0)
            {
                res.push_back(nums[buffer.front()]);
            }
            
        }
        
        return res;
    }
};
```