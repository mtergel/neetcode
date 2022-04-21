```cpp
// Problem: https://leetcode.com/problems/kth-largest-element-in-a-stream/
// Time: O(N * logN)
// Space: O(K)

class KthLargest {
private:
    priority_queue<int, vector<int>, greater<int>> minheap;
    int kth;
public:
    KthLargest(int k, vector<int>& nums) {
        kth = k;
        for (int num : nums)
        {
           add(num);
        }
    }
    
    int add(int val) {
        if (minheap.size() < kth)
        {
            minheap.push(val);
        }
        else
        {
            if (val > minheap.top())
            {
                minheap.pop();
                minheap.push(val);
            }
        }
        
        return minheap.top();
    }
};

```