```cpp
// Problem: https://leetcode.com/problems/clone-graph
// Time: O(N)
// Space: O(N)

/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/
class Solution {
public:
    Node* cloneGraph(Node* node) {
        if (node == nullptr)
        {
            return node;
        }

        // value <-> cloned address
        unordered_map<int, Node*> clones;

        queue<Node*> toCheck;
        toCheck.push(node);

        Node* clone = new Node(node->val);
        clones.insert({clone->val, clone});

        while (!toCheck.empty())
        {
            Node* curr = toCheck.front();
            toCheck.pop();

            // check neighbours
            for (Node* neigh : curr->neighbors)
            {
                if (clones.find(neigh->val) == clones.end())
                {
                    Node* clone = new Node(neigh->val);
                    clones.insert({clone->val, clone});

                    // add it for checking next
                    toCheck.push(neigh);

                }

                // add the cloned neighbors to
                // the current cloned node
                clones[curr->val]->neighbors.push_back(clones[neigh->val]);
            }
        }

        return clone;
    }
};
```