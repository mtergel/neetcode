```cpp
// Problem: https://leetcode.com/problems/design-add-and-search-words-data-structure

class TrieNode {
public:
    bool isEnd;
    vector<TrieNode*> links;
    
    
    TrieNode() {
        isEnd = false;
        links.resize(26, nullptr);
    }
};

class WordDictionary {
private:
    TrieNode* root;
    
    bool searchHelper(string word, TrieNode* curr)
    {
        for (int i = 0; i < word.size(); i++)
        {
            if (word[i] == '.')
            {
                bool found = false;
                int j = 0;
                while (j < 26)
                {
                    if (curr->links[j])
                    {
                        found = found || searchHelper(word.substr(i + 1), curr->links[j]);
                    }
                    
                    if (found)
                    {
                        return true;
                    }
                    
                    j++;
                }
                
                return false;
            }
            else
            {
                if (curr->links[word[i] - 'a'] == nullptr)
                {
                    return false;
                }
                
                curr = curr->links[word[i] - 'a'];
            }
        }
        
        return curr->isEnd;
    }
    
    
public:
    WordDictionary() {
        root = new TrieNode();
    }
    
    void addWord(string word) {
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
    }
    
    bool search(string word) {
        return searchHelper(word, root);
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary* obj = new WordDictionary();
 * obj->addWord(word);
 * bool param_2 = obj->search(word);
 */
```