```cpp
// Problem: https://leetcode.com/problems/hand_of_straights
// Time: O(N)
// Space: O(1)

class Solution {
public:
    bool mergeTriplets(vector<vector<int>>& triplets, vector<int>& target) {
        // if any triplet with greater value than target
        // ignore it
        // check if target's numbers is in any triplets
        
        bool first = false, sec = false, third = false;
      
        for (vector<int> triplet : triplets)
        {
            if (triplet[0] == target[0] && (triplet[1] <= target[1] && triplet[2] <= target[2]))
            {
                first = true;
            }
            
            if (triplet[1] == target[1] && (triplet[0] <= target[0] && triplet[2] <= target[2]))
            {
                sec = true;
            }
            
            if (triplet[2] == target[2] && (triplet[0] <= target[0] && triplet[1] <= target[1]))
            {
                third = true;
            }
        }
        
        return first && sec && third;
    }
};
```