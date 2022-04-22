```cpp
// Problem: https://leetcode.com/problems/time-based-key-value-store/
// Time: O(logn)
// Space: O(1)

class TimeMap {
private:
    unordered_map<string, vector<pair<int, string>>> mp;
    
public:
    TimeMap() {
        
    }
    
    void set(string key, string value, int timestamp) {
        mp[key].push_back({timestamp, value});
    }
    
    string get(string key, int timestamp) {
        auto& valpair = mp[key];
        int start = 0;
        int end = valpair.size() - 1;
        while(start <= end)
        {
            int mid = start+(end-start)/2;
            valpair[mid].first > timestamp ? end = mid-1 : start = mid+1; // 'end' will be equal or one less of TS
        }
        return end < 0 ? "" : valpair[end].second;
    }
};
```