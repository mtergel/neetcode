```cpp
// Problem: https://leetcode.com/problems/task-scheduler
// Time: O(N)
// Space: O(26)

// or can use heap + queue + time variable
// idea is count the tasks
// and pop them into the queue + interval
// when item is up in the queue pop it back into the heap

class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        vector<int> count(26, 0);
        int largest = 0;
        
        for (char c : tasks)
        {
            count[c - 'A']++;
        }
        
        int maxcount = *max_element(count.begin(), count.end());
        for (int i = 0; i < 26; i++)
        {
            if (count[i] == maxcount)
            {
                largest++;
            }
        }
        
        // have to choose atleast maxcount rounds
        // maxcount - 1 comes from the last queue not requiring interval
        // n + 1 the gaps

        // AB___AB___AB___AB___AB___AB

        return max((int)tasks.size(), (maxcount - 1) * (n + 1) + largest);
    }
};
```