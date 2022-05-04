```cpp
// Problem: https://leetcode.com/problems/swim-in-rising-water

class Solution {
public:
    unordered_map<char, set<char>> adj;
    // false = visited
    // true = in current path
    unordered_map<char, bool> visited;
    
    bool dfs(vector<char>& res, char c)
    {
        if (visited.find(c) != visited.end())
        {
            return visited[c];
        }

        visited[c] = true;

        for (auto neigh : adj[c])
        {
            if (dfs(res, neigh))
            {
                return true;
            }
        }

        visited[c] = false;
        res.push_back(c);
    }
    string alienOrder(vector<string> &words) {

        for (auto word : words)
        {
            for (auto c : word)
            {
                adj[c] = {};
            }
        }

        for (int i = 0; i < words.size() - 1; i++)
        {
            string w1 = words[i];
            string w2 = words[i + 1];
            int minLen = min(w1.size(), w2.size());
            if (w1.size() > w2.size() &&
                w1.substr(0, minLen) == w2.substr(0, minLen)
            )
            {
                // invalid ordering
                return "";
            }

            for (int j = 0; j < minLen; j++)
            {
                if (w1[j] != w2[j])
                {
                    adj[w1[j]].insert(w2[j]);
                    break;
                }
            }
        }

        vector<char> res;
        for (auto& it : adj)
        {
            if (dfs(res, it.first))
            {
                cout << it.first;
                return "";
            }
        }

        reverse(res.begin(), res.end());
        string resString = "";
        for (auto c : res)
        {
            resString += c;
        }
    
        return resString;
    }
};
```