```cpp
// Problem: https://leetcode.com/problems/lru-cache
// Time: O(N)
// Space: O(1) 

class LRUCache {
private:
    int cacheCap;

    // front = most recently used
    // back = least recently used
    list<pair<int, int>> nodes;

    unordered_map<int, list<pair<int, int>>::iterator> cache;
    
public:
    LRUCache(int capacity) {
        cacheCap = capacity;
    }
    
    int get(int key) {
        if (cache.find(key) == cache.end())
        {
            return -1;
        }
        
        // puts cache[key] at the front
        nodes.splice(nodes.begin(), nodes, cache[key]);
        
        return cache[key]->second;
    }
    
    void put(int key, int value) {
        if (cache.find(key) != cache.end())
        {
            nodes.splice(nodes.begin(), nodes, cache[key]);
            cache[key]->second = value;
            return;
        }
        
        if (nodes.size() == cacheCap)
        {
            auto lru = nodes.back().first;
            nodes.pop_back();
            cache.erase(lru);
        }
        
        // add new node
        nodes.push_front({key, value});
        cache[key] = nodes.begin();
    }
};
```