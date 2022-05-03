```cpp
// Problem: https://leetcode.com/problems/find-median-from-data-stream
// Time: O(logn) limited to logK when **minheap** size is limited to K
// Space: O(N)

// idea use two heaps
// one for max values 1, 2, 3
// one for min values 4, 5, 6
// so you can get 3, 4 in O(1) time

class MedianFinder {
private:
    priority_queue<int> maxh;
    priority_queue<int, vector<int>, greater<int>> minh;
    
    void balanceHeaps() {
        if (maxh.size() > minh.size() + 1)
        {
            minh.push(maxh.top());
            maxh.pop();
        }
        
        if (minh.size() > maxh.size() + 1)
        {
            maxh.push(minh.top());
            minh.pop();
        }
    }
    
public:
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        // try to keep the size between the
        // two heaps <= 1

        // default case, num belongs in the smaller half
        if (maxh.empty() || maxh.top() > num)
        {
            maxh.push(num);
        }
        else
        {
            minh.push(num);
        }
        
        balanceHeaps();
        
    }
    
    double findMedian() {
        if (maxh.size() == minh.size())
        {
            if (maxh.empty())
            {
                return 0;
            }
            else
            {
                return (maxh.top() + minh.top()) / 2.0;
            }
        }
        else
        {
            return maxh.size() > minh.size() ? maxh.top() : minh.top();
        }
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```