```cpp
// Problem: https://leetcode.com/problems/top-k-frequent-elements/
// Time O(N)   / O(NlogK) for heap solution 
// Space O(N)  / O(N + k) for heap

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        int n = nums.size();
        if (k >= n)
        {
            return nums;
        }
        
        
        unordered_map<int, int> count;
        vector<vector<int>> freq(n + 1);
        
        for (int num : nums)
        {
            count[num]++;
        }
        
        for (auto it = count.begin(); it != count.end(); it++)
        {
            freq[it->second].push_back(it->first);
        }
        
        vector<int> res;
        res.reserve(k);
        
        bool finished = false;
        
        for (int i = n; i >= 0; i--)
        {
            if (finished)
            {
                break;
            }
            
            for (int num : freq[i])
            {
                if (res.size() == k)
                {
                    finished = true;
                    break;
                }
                res.push_back(num);
            }
        }
        
        return res;
    }
};
```