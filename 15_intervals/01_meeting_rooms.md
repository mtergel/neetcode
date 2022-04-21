```cpp
// Problem: https://www.lintcode.com/problem/920/
// Time: O(NlogN)
// Space: O(1)

/**
 * Definition of Interval:
 * class Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this->start = start;
 *         this->end = end;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param intervals: an array of meeting time intervals
     * @return: if a person could attend all meetings
     */
    bool canAttendMeetings(vector<Interval> &intervals) {
        if (intervals.size() <= 1)
        {
            return true;
        }

        sort(intervals.begin(), intervals.end(), 
        [](const Interval &lhs, const Interval &rhs) -> bool {
            return lhs.start <= rhs.start;
        });

        for (int i = 0; i < intervals.size() - 1; i++)
        {
            if (intervals[i].end > intervals[i + 1].start)
            {
                return false;
            }
        }

        return true;
    }
};
```