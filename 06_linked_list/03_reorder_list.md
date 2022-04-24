```cpp
// Problem: https://leetcode.com/problems/reorder-list/
// Time: O(N)
// Space: O(1)
class Solution {
public:
    ListNode* reverse(ListNode* root)
    {
        ListNode* prev = nullptr;
        ListNode* curr = root;
        ListNode* next;
        
        while (curr)
        {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        
        return prev;
    }
    
    void reorderList(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
        {
            return;
        }
        
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast && fast->next && fast->next->next)
        {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        ListNode* half = reverse(slow->next);
        slow->next = nullptr;
        
        ListNode* curr = head;
        
        while (curr && half)
        {
            ListNode* currNext = curr->next;
            ListNode* halfNext = half->next;
            
            curr->next = half;
            half->next = currNext;
            
            curr = currNext;
            half = halfNext;
        }
        
    }
};
```