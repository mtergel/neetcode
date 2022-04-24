```cpp
// Problem: https://leetcode.com/problems/add-two-numbers
// Time: O(max(N, M))
// Space: O(max(N, M)) 

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        int carry = 0;
        ListNode sum(0);
        ListNode* curr = &sum;
        
        while (l1 || l2)
        {
            int digitSum = (l1 != nullptr ? l1->val : 0) + (l2 != nullptr ? l2->val : 0) + carry;
            carry = digitSum / 10;
            curr->next = new ListNode(digitSum % 10);
            curr = curr->next;
            
            if (l1)
            {
                l1 = l1->next;
            }
            
            if (l2)
            {
                l2 = l2->next;
            }
        }
        
        if (carry > 0)
        {
            curr->next = new ListNode(carry);
        }
        
        return sum.next;
    }
};
```