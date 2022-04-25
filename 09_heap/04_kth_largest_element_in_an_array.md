```cpp
// Problem: https://leetcode.com/problems/kth-largest-element-in-an-array
// Time: ~O(N), O(N^2)
// Space: O(1)

class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        k = nums.size() - k;
        return quickSelect(nums, 0, nums.size() - 1, k);
    }
private:
    // nums, l pointer, r pointer, kth index
    int quickSelect(vector<int>& nums, int l, int r, int k) {
        int pivot = nums[r];
        int p = l;
        
        for (int i = l; i < r; i++)
        {
            if (nums[i] <= pivot)
            {
                swap(nums[p], nums[i]);
                p++;
            }
        }
        
        // swapping pivot with p pointer
        swap(nums[p], nums[r]);
        
        if (p > k)
        {
            // look at the left portion
            return quickSelect(nums, l, p - 1, k);
        }
        else if (p < k)
        {
            // look at the right portion
            return quickSelect(nums, p + 1, r, k);
        }
        
        return nums[p];
    }
};
```