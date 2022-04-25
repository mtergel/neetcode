```cpp
// Problem: https://leetcode.com/problems/subsets
// Time: O(N * M * ?)
// Space: O(N)

class Solution {
private:
    vector<vector<bool>> visited;
    bool dfs(int i, int j, int start, string& word, vector<vector<char>>& board)
    {
        if (start == word.size())
        {
            return true;
        }
        
        if (i < 0 || j < 0 || i >= board.size() || j >= board[0].size() || 
            word[start] != board[i][j] || 
            visited[i][j]
           )
        {
            return false;
        }
        
        visited[i][j] = true;
        bool res =  dfs(i + 1, j, start + 1, word, board) ||
                    dfs(i - 1, j, start + 1, word, board) ||
                    dfs(i, j + 1, start + 1, word, board) ||
                    dfs(i, j - 1, start + 1, word, board);
        
        visited[i][j] = false;
        return res;
    }
    
public:
    bool exist(vector<vector<char>>& board, string word) {
        
        int m = board.size();
        int n = board[0].size();
        
        // prune #1
        // check if grid has enough letter
        if (word.size() > m * n)
        {
            return false;
        }
        
        // prune #2
        // check if grid has enough letter for words
        unordered_map<char, int> charCount;
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                charCount[board[i][j]]++;
            }
        }
        
        for (int i = 0; i < word.size(); i++)
        {
            if (charCount.find(word[i]) == charCount.end())
            {
                return false;
            }
            else
            {
                if (charCount[word[i]] == 1)
                {
                    charCount.erase(word[i]);
                }
                else
                {
                    charCount[word[i]]--;
                }
            }
        }
        
        
        visited = vector(m, vector(n, false));
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (dfs(i, j, 0, word, board))
                {
                    return true;
                }
            }
        }
        
        return false;
    }
};
```