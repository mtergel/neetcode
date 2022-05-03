
```cpp
// Problem: https://leetcode.com/problems/word-search-ii/

class TrieNode {
public:
    bool isEnd;
    vector<TrieNode*> links;
    int wordIdx;
    
    TrieNode() 
    {
        isEnd = false;
        links.resize(26, nullptr);
        wordIdx = 0;
    }
};

class Trie {
private:
    TrieNode* root;
    
public:
    Trie() 
    {
        root = new TrieNode();
    }
    
    TrieNode* getRoot()
    {
        return root;
    }
    
    void insert(string word, int wordIdx)
    {
        TrieNode* curr = root;
        for (int i = 0; i < word.size(); i++)
        {
            if (curr->links[word[i] - 'a'] == nullptr)
            {
                curr->links[word[i] - 'a'] = new TrieNode();
            }
            
            curr = curr->links[word[i] - 'a'];
        }
        
        curr->isEnd = true;
        curr->wordIdx = wordIdx;
    }
};

class Solution {
private:
    vector<string> res;
    void dfs(vector<vector<char>>& board, vector<string>& words, TrieNode* curr, int i, int j)
    {
        char c = board[i][j];
        if (c == '#' || curr->links[c - 'a'] == nullptr)
        {
            return;
        }
        
        // try next letter
        curr = curr->links[c - 'a'];
        if (curr->isEnd)
        {
            res.push_back(words[curr->wordIdx]);
            
            // remove duplicate e.g mark word as visited
            curr->isEnd = false;
        }
        
        board[i][j] = '#';
        if (i > 0)
        {
            dfs(board, words, curr, i - 1, j);
        }
        if (j > 0)
        {
            dfs(board, words, curr, i, j - 1);
        }
        if (i < board.size() - 1)
        {
            dfs(board, words, curr, i + 1, j);
        }
        if (j < board[0].size() - 1)
        {
            dfs(board, words, curr, i, j + 1);
        }
        
        board[i][j] = c;
    }
    
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        Trie* trie = new Trie();
        for (int i = 0; i < words.size(); i++)
        {
            trie->insert(words[i], i);
        }
        
        TrieNode* root = trie->getRoot();
        
        int m = board.size();
        int n = board[0].size();
        
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dfs(board, words, root, i, j);
            }
        }
        
        delete root;
        delete trie;
        
        return res;
    }
};
```