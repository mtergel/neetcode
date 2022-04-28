```cpp
// Problem: https://leetcode.com/problems/min-cost-to-connect-all-points/
// Time: Prim O(n^2 logn)
// n^2 <- connecting nodes
// logn <- for heap

// if Optimized O(n^2)
// Space: O(N) ? 

class Solution {
public:

    // optimized prim's algo
    int minCostConnectPoints(vector<vector<int>>& points) {
        int n = points.size();
        
        vector<int> minDist(n, INT_MAX);
        minDist[0] = 0;
        
        int mstCost = 0;
        int edgesUsed = 0;
        vector<bool> inMST(n, false);
        
        while (edgesUsed < n)
        {
            int currMinEdge = INT_MAX;
            int currNode = -1;
            
            for (int node = 0; node < n; node++)
            {
                if (!inMST[node] && currMinEdge > minDist[node])
                {
                    currMinEdge = minDist[node];
                    currNode = node;
                }
            }
            
            mstCost += currMinEdge;
            edgesUsed++;
            inMST[currNode] = true;
            
            // update neighbours
            for (int nextNode = 0; nextNode < n; nextNode++)
            {
                int weight = abs(points[nextNode][0] - points[currNode][0]) +
                    abs(points[nextNode][1] - points[currNode][1]);
            
                if (!inMST[nextNode] && minDist[nextNode] > weight)
                {
                    minDist[nextNode] = weight;
                }
            }
        }
        
        return mstCost;
    }
};

```