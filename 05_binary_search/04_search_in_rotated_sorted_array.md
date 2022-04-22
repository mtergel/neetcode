```cpp
// Problem: https://leetcode.com/problems/search-in-rotated-sorted-array/
// Time: O(logn)
// Space: O(1)

class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        
        while (l <= r)
        {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target)
            {
                return mid;
            }
            
            if (nums[mid] > nums[r])
            {
                // rotation
                // its in the left half of the rotation
                if (target < nums[mid] && target >= nums[l])
                {
                    r = mid - 1;
                }
                else
                {
                    l = mid + 1;
                }
                
            }
            else if (nums[mid] < nums[l])
            {
                // rotation
                if (target > nums[mid] && target <= nums[r])
                {
                    l = mid + 1;
                }
                else
                {
                    r = mid - 1;
                }
            }
            else
            {
                // normal
                if (nums[mid] > target)
                {
                    r = mid - 1;
                }
                else
                {
                    l = mid + 1;
                }
            }
        }
        
        return -1;
    }
};
```