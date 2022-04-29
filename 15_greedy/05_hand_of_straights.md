```cpp
// Problem: https://leetcode.com/problems/hand_of_straights
// Time: O(N)
// Space: O(N) can be reduced to O(1)

class Solution {
public:
    bool isNStraightHand(vector<int>& hand, int groupSize) {
        int n = hand.size();
        if (n % groupSize)
        {
            return false;
        }
        
        // card, count
        map<int, int> count;
        for (int num : hand) // O(N)
        {
            count[num]++; // O(logN)
        }
        
        
        while (!count.empty())
        {
            int curr = count.begin()->first;
            for (int i = curr; i < curr + groupSize; i++)
            {
                if (count.find(i) == count.end())
                {
                    return false;
                }
                
                count[i]--;
                if (count[i] == 0)
                {
                    // e.g 1 1 2 3
                    // create the 1 2 3
                    
                    // but the next 1 doesnt have a 2
                    // anymore
                    if (i != count.begin()->first)
                    {
                        return false;
                    }
                    count.erase(i);
                }
            }
        }
        
        return true;
    }
};
```