```cpp
// Problem: https://www.lintcode.com/problem/919/
// Time: O(N)
// Space: O(N)

/**
 * Definition of Interval:
 * class Interval {
 * public:
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
     * @return: the minimum number of conference rooms required
     */
    int minMeetingRooms(vector<Interval> &intervals) {
        // line sweep techinque
        map<int, int> m;

        for (auto interval : intervals)
        {
            m[interval.start]++;
            m[interval.end]--;
        }

        int count = 0;
        int roomCount = 0;
        for (auto it = m.begin(); it != m.end(); it++)
        {
            count += it->second;
            roomCount = max(roomCount, count);
        }

        return roomCount;
    }
};
```