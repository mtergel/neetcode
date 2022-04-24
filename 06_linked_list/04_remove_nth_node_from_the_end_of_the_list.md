```cpp
// Problem: https://leetcode.com/problems/remove-nth-node-from-end-of-list
// Time: O(N)
// Space: O(1) 

class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        int delay = 0;
        
        ListNode dummy(-1, head);
        ListNode* prev = &dummy;
        ListNode* delayed = head;
        ListNode* curr = head;
        
        while (curr)
        {
            if (delay == n)
            {
                delayed = delayed->next;
                prev = prev->next;
            }
            else
            {
                delay++;
            }
            
            curr = curr->next;
        }
        
        // skip the delayed node nth node from the end of the list
        prev->next = delayed->next;
        
        // free memory
        delete delayed;
        
        return dummy.next;
    }
};
```