```cpp
// Problem: https://leetcode.com/problems/valid-anagram/
// Time (hashmap / sorting): O(N) / O(NlogN)
// Space (hashmap / sorting): O(N) / O(1)

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // num, index
        unordered_map<int, int> seen;
        vector<int> res;
        
        for (int i = 0; i < nums.size(); i++)
        {
            if (seen.find(target - nums[i]) != seen.end())
            {
                res = {i, seen[target - nums[i]]};
                break;
            }
            else
            {
                seen.insert({nums[i], i});
            }
        }
        
        return res;
    }
};
```