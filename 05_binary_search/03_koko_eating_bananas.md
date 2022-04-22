```cpp
// Problem: https://leetcode.com/problems/koko-eating-bananas/
// Time: O(N * logM) (range 1 - M)
// Space: O(1)

class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int l = 1;
        int r = *max_element(piles.begin(), piles.end());
        
        while (l < r)
        {
            int mid = l + (r - l) / 2;
            int eatingHour = 0;
            
            for (int pile : piles)
            {
                // ceil gives precision
                eatingHour += pile / mid + (pile % mid != 0);
                
                // can't eat everything
                // try next
                if (eatingHour > h)
                {
                    break;
                }
            }
            
            if (eatingHour <= h)
            {
                r = mid;
            }
            else
            {
                l = mid + 1;
            }
            
        }
        
        return r;
        
    }
};
```