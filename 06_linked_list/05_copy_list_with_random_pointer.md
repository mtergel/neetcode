```cpp
// Problem: https://leetcode.com/problems/copy-list-with-random-pointer/
// Time: O(N)
// Space: O(1) 

class Solution {
public:
    Node* copyRandomList(Node* head) {
// if we are using extra space

//         // original node <-> cloned node
//         unordered_map<Node*, Node*> cloned;

//         Node* curr = head;
//         while (curr)
//         {
//             Node* clone = new Node(curr->val);
//             cloned.insert({curr, clone});

//             curr = curr->next;
//         }

//         curr = head;
//         while (curr)
//         {
//             if (curr->next)
//             {
//                 cloned[curr]->next = cloned[curr->next];
//             }

//             if (curr->random)
//             {
//                 cloned[curr]->random = cloned[curr->random];
//             }

//             curr = curr->next;
//         }

//         return cloned[head]; 
        
        // no extra space
        // tweaking the original linked list -> interweave the nodes
        
        Node *l2Root, *l1, *l2;
        if (head == nullptr) 
            return head;
        
        // copying nodes
        for (l1 = head; l1 != nullptr; l1 = l1->next->next)
        {
            l2 = new Node(l1->val);
            l2->next = l1->next;
            l1->next = l2;
        }
        
        // the first l2
        l2Root = head->next;
        
        // copying random pointers
        for (l1 = head; l1 != nullptr; l1 = l1->next->next)
        {
           if (l1->random != nullptr)
           {
               // cloned nodes (l2) = copied random
               l1->next->random = l1->random->next;
           }
        }
        
        // picking the copied nodes over to l2
        for (l1 = head; l1 != nullptr; l1 = l1->next)
        {
            l2 = l1->next;
            
            // skip the cloned node
            l1->next = l2->next;
            
            if (l2->next != nullptr)
            {
                l2->next = l2->next->next;
            }
        }
        
        return l2Root;
    }
};
```