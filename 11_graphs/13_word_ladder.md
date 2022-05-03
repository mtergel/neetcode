```cpp
// Problem: https://leetcode.com/problems/number-of-provinces
// Time: O (V + E)
// Space: O(V + E)

// for some reason I cant code the iterative version

class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        const char letters [26] = {'a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'};
        
        unordered_set<string> dict(wordList.begin(), wordList.end());
        dict.insert(beginWord);
        
        if (dict.find(endWord) == dict.end())
        {
            return 0;
        }
        
        queue<string> q;
        q.push(beginWord);
        int step = 0;
        
        while (!q.empty())
        {
            int size = q.size();
            while (size--)
            {
                string curr = q.front();
                q.pop();
                
                if (curr == endWord)
                {
                    return step + 1;
                }
                
                dict.erase(curr);
                for (int i = 0; i < curr.size(); i++)
                {
                    char tmp = curr[i];
                    for (int j = 0; j < 26; j++)
                    {
                        curr[i] = letters[j];
                        if (dict.find(curr) != dict.end())
                        {
                            dict.erase(curr);
                            q.push(curr);
                        }
                        curr[i] = tmp;
                    }
                }
            }
            step++;
        }
        
        return 0;
    }
};
```