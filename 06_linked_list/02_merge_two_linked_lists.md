```cpp
// Problem: https://leetcode.com/problems/merge-two-sorted-lists/submissions/
// Time: O(N + M) N, M beigning list sizes
// Space: O(1), O(N + M) for call stack if recursivly solved 
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        
        ListNode dummy(-1);
        ListNode* prev = &dummy;
        ListNode* p1 = list1;
        ListNode* p2 = list2;
        
        while (p1 && p2)
        {
            if (p1->val > p2->val)
            {
                prev->next = p2;
                p2 = p2->next;
            }
            else
            {
                prev->next = p1;
                p1 = p1->next;
            }
            
            prev = prev->next;
        }
        
        if (p1)
        {
            prev->next = p1;
        }
        else if (p2)
        {
            prev->next = p2;
        }
        
        return dummy.next;
    }
};
```