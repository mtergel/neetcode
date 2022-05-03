```cpp
// Problem: https://leetcode.com/problems/lru-cache
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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2)
    {
        if (list1 == nullptr)
        {
            return list2;
        }
        
        if (list2 == nullptr)
        {
            return list1;
        }
        
        ListNode dummy(-101, list1);
        ListNode *curr = &dummy;
        
        ListNode* p1 = list1;
        ListNode* p2 = list2;
        
        while (p1 && p2)
        {
            if (p1->val < p2->val)
            {
                curr->next = p1;
                p1 = p1->next;
            }
            else
            {
                curr->next = p2;
                p2 = p2->next;
            }
            
            curr = curr->next;
        }
        
        if (p1 == nullptr)
        {
            curr->next = p2;
        }
        else
        {
            curr->next = p1;
        }
        
        return dummy.next;
            
    };
    
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if (lists.empty())
        {
            return NULL;
        }
        
        int size = lists.size();
        
        while (size > 1)
        {
            for (int i = 0; i < size / 2; i++)
            {
               lists[i] = mergeTwoLists(lists[i], lists[size - i - 1]);
            }
            
            size = (size + 1) / 2;
        }
        
        return lists.front();
        
    }
};
```