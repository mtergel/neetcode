```cpp
// Problem: https://leetcode.com/problems/linked-list-cycle
// Time: O(N)
// Space: O(1) 

class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == nullptr)
        {
            return false;
        }
        
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast && fast->next && fast->next->next)
        {
            slow = slow->next;
            fast = fast->next->next;
            
            if (slow == fast)
            {
                return true;
            }
        }
        
        return false;
    }
};
```