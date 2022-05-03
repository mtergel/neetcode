```cpp
// Problem: https://leetcode.com/problems/reverse-nodes-in-k-group
// Time: O(N)
// Space: O(1) 

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
private:
    ListNode* reverseList(ListNode* root, int k)
    {
        ListNode* prev = nullptr;
        ListNode* curr = root;
        
        while (curr && k > 0)
        {
            ListNode* next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
            
            k--;
        }
        
        return prev;
    }
    
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (head == nullptr || head->next == nullptr || k == 0 || k == 1)
        {
            return head;
        }
        
        ListNode dummy(-1, head);
        ListNode* prev = &dummy;
        ListNode* curr = head;
        
        while (curr)
        {
            ListNode* tail = curr;
            int count = 0;
            while (curr && count < k)
            {
                curr = curr->next;
                count++;
            }
            
            // ended before we could
            // get the kth cycle
            if (count != k)
            {
                prev->next = tail;
            }
            else
            {
                prev->next = reverseList(tail, k);
                prev = tail;
            }
            
        }
        
        return dummy.next;
    }
};
```