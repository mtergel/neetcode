```cpp
// Problem: https://leetcode.com/problems/k-closest-points-to-origin/
// Time: O(N * logK) limited to logK when **minheap** size is limited to K
// Space: O(K)

class Twitter {
private:
    // userId, followeeIds
    unordered_map<int, unordered_set<int>> follows;
    
    // userId, tweets
    // tweets ->   time <-> tweetId
    unordered_map<int, vector<pair<int,int>>> tweets;
        
    int time;
    int k;
    
    
public:
    Twitter() {
        time = 0;
        k = 10;
    }
    
    void postTweet(int userId, int tweetId) {
    
        tweets[userId].push_back({time, tweetId});
        time++;
    }
    
    vector<int> getNewsFeed(int userId) {
        
        // heap comp
        auto comp = [](const pair<int, int>& lhs, const pair<int, int>& rhs) {
            return lhs.first < rhs.first;
        };
        
        vector<int> res;
        
        unordered_set<int> &followees = follows[userId];
        // priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(comp)> pq(comp);
        priority_queue<pair<int, int>> pq;
        
        // but get the last if possible k
        int count = 0;
        for (auto it = tweets[userId].rbegin(); it != tweets[userId].rend(); it++)
        {
            if (count++ == k)
            {
                break;
            }
            pq.push(*it);
        }

        // followed users
        for (auto it = followees.begin(); it != followees.end(); it++)
        {
            // get followee's tweets
            vector<pair<int, int>> &followeeTweets = tweets[*it];
            
            count = 0;
            for (auto it = followeeTweets.rbegin(); it != followeeTweets.rend(); it++)
            {
                if (count++ == k)
                {
                    break;
                }
                pq.push(*it);
            }
        }
        
        count = 10;
        while (!pq.empty() && count--)
        {
                res.push_back(pq.top().second);
                pq.pop();
        }
        
        return res;
    }
    
    void follow(int followerId, int followeeId) {
        if (followerId != followeeId)
        {
            follows[followerId].insert(followeeId);
        }
    }
    
    void unfollow(int followerId, int followeeId) {        
        follows[followerId].erase(followeeId);
    }
};

```