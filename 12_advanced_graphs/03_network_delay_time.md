```cpp
// Problem: https://leetcode.com/problems/network-delay-time/
// Time: O(N + E logN)
// Space: O(N + E)

class Solution {
private:
    vector<pair<int, int>> adj[101];
    
    void dijsktra(vector<int>& signalReceivedAt, int source, int n) 
    {
        priority_queue<pair<int, int>, vector<pair<int, int>>, 
            greater<pair<int, int>>> pq;
        
        pq.push({0, source});
        
        signalReceivedAt[source] = 0;
        
        while (!pq.empty())
        {
            int currNodeTime = pq.top().first;
            int currNode = pq.top().second;
            
            pq.pop();
            
            if (currNodeTime > signalReceivedAt[currNode])
            {
                continue;
            }
            
            // broadcast the signal to adj nodes
            for (auto edge : adj[currNode])
            {
                int time = edge.first;
                int neigh = edge.second;
                
                // fastest signal
                if (signalReceivedAt[neigh] > currNodeTime + time)
                {
                    signalReceivedAt[neigh] = currNodeTime + time;
                    pq.push({signalReceivedAt[neigh], neigh});
                }
            }
        }
    }
    
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        
        for (vector<int> time : times)
        {
            int source = time[0];
            int dest = time[1];
            int travelTime = time[2];
            
            adj[source].push_back({travelTime, dest});
        }
        
        vector<int> signalReceivedAt(n + 1, INT_MAX);
        dijsktra(signalReceivedAt, k, n);
        
        int res = INT_MIN;
        for (int i = 1; i <= n; i++)
        {
            res = max(res, signalReceivedAt[i]);
        }
                
        return res == INT_MAX ? -1 : res;
    }
};
```