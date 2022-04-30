```cpp
// Problem: https://leetcode.com/problems/detect-squares/
// Time: O(N)
// Space: O(N)

class DetectSquares {
private:
    map<pair<int, int>, int> points;
    bool isValid(int x, int y, int x1, int y1)
    {
        return abs(x - x1) == abs(y - y1);
    }
    
public:
    DetectSquares() {
        
    }
    
    void add(vector<int> point) {
       points[{point[0], point[1]}]++;
    }
    
    int count(vector<int> point) {
        int res = 0;
        int px = point[0];
        int py = point[1];
        
        for (auto it : points)
        {
            auto [x, y] = it.first;
            if (x != px && y != py &&
               isValid(x, y, px, py)
                )
            {
                int duplicateCount = 1;
                duplicateCount *= points[{x, py}];
                duplicateCount *= points[{px, y}];
                duplicateCount *= points[{x, y}];
                
                res += duplicateCount;
            }
        }
        
        
        return res;
    }
};

/**
 * Your DetectSquares object will be instantiated and called as such:
 * DetectSquares* obj = new DetectSquares();
 * obj->add(point);
 * int param_2 = obj->count(point);
 */
```