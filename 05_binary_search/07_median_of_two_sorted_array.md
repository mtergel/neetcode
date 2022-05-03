```cpp
// Problem: https://leetcode.com/problems/binary-search/
// Time: O(logN)
// Space: O(1)

class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        // 2 partition
        // of (n1 + n2) / 2 size
        
        // the median is
        // the max of first partition (nums1, nums2)
        // the min of the second partition (nums1, nums2)
        
        // in other words
        // if we can find how many elements of each array is in each partition
        // we can find the median
        
        // to find the median
        // given
        
        // [1, 5, 8, 10, 18, 20]
        // [2, 3, 6, 7]
        
        // 1 2 3 5 6    |   7 8 10 18 20
        
        // l partition     r partition
        // 1 5              8 10 18 20
        // 2 3 6            7
        
        // l1 = 5
        // l2 = 6
        // r1 = 8
        // r2 = 7
        
        // when l1 <= r2 && l2 <= r1 is correct partition is correct

        vector<int> a(nums1.begin(), nums1.end());
        vector<int> b(nums2.begin(), nums2.end());
        
        int m = a.size();
        int n = b.size();
        
        if (m > n)
        {
            swap(m, n);
            swap(a, b);
        }
        
        int total = m + n;
        int half = (total + 1) / 2;
        
        int l = 0, r = m;
        while (l <= r)
        {
            int cut1 = l + (r - l) / 2;
            int cut2 = half - cut1;
            int l1 = cut1 == 0 ? INT_MIN : a[cut1 - 1];
            int r1 = cut1 == m ? INT_MAX : a[cut1];
            
            int l2 = cut2 == 0 ? INT_MIN : b[cut2 - 1];
            int r2 = cut2 == n ? INT_MAX : b[cut2];
            
            if (l1 <= r2 && l2 <= r1){
                if (total % 2 == 0)
                    return (double)(max(l1, l2) + min(r1, r2)) / 2;
                else
                    return (double)(max(l1, l2));
                
            } else if (l1 > r2)
                r = cut1 - 1;
            else
                l = cut1 + 1;
        }
        
        return -1.0;
    }
};
```