```cpp
// Problem: https://leetcode.com/problems/implement-trie-prefix-tree/

// Insert O(M) m - key length O(M)
// Search O(M) O(1)
// Search prefix O(M) O(1)

class TrieNode {
public:
    bool isEnd;
    vector<TrieNode*> links;
    
    TrieNode() {
        isEnd = false;
        links.resize(26, nullptr);
    }
    
};


class Trie {
public:
    TrieNode* root;
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* curr = root;
        for (int i = 0; i < word.size(); i++)
        {
            if (curr->links[word[i] - 'a'] == nullptr)
            {
                curr->links[word[i] -'a'] = new TrieNode();
            }
            
            // check next
            curr = curr->links[word[i] - 'a'];
        }
        
        // mark end
        curr->isEnd = true;
    }
    
    bool search(string word) {
        TrieNode* curr = root;
        
        for (int i = 0; i < word.size(); i++)
        {
            TrieNode* node = curr->links[word[i] - 'a'];
            if (node == nullptr)
            {
                return false;
            }
            
            curr = node;
        }
        
        return curr->isEnd;
    }
    
    bool startsWith(string prefix) {
        TrieNode* curr = root;
        
        for (int i = 0; i < prefix.size(); i++)
        {
            TrieNode* node = curr->links[prefix[i] - 'a'];
            if (node == nullptr)
            {
                return false;
            }
            
            curr = node;
        }
        
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```