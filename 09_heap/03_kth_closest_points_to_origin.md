```cpp
// Problem: https://leetcode.com/problems/k-closest-points-to-origin/
// Time: O(N * logK) limited to logK when heap size is limited to K
// Space: O(K)

class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        
        // distance, index
        priority_queue<pair<int, int>> pq;
        
        for (int i = 0; i < points.size(); i++)
        {
            pair<int, int> entry = {getDist(points[i]), i};
            if (pq.size() < k)
            {
                pq.push(entry);
            }
            else if (entry.first < pq.top().first)
            {
                pq.pop();
                pq.push(entry);
            }
        }
        
        vector<vector<int>> res;
        while (!pq.empty())
        {
            res.push_back(points[pq.top().second]);
            pq.pop();
        }
        
        return res;
    }
    
private:
    int getDist(vector<int>& point)
    {
        return point[0] * point[0] + point[1] * point[1];
    }
};


```