# Top View of a Binary Tree 

Given a **binary tree**, print its **Top View**.

### Definition  
The **Top View** of a binary tree is the set of nodes visible when the tree is viewed from the **top**.

- For each **horizontal distance (HD)** from the root, only the **first node encountered** (topmost) is included.
- Nodes are printed from **leftmost HD to rightmost HD**.

---


## Core Idea (Level Order + Horizontal Distance)

We use **Level Order Traversal (BFS)** because:
- BFS ensures we visit nodes **top to bottom**
- The first node encountered at a horizontal distance is the top view node

### Horizontal Distance (HD)
- Root → HD = `0`
- Left child → HD = `parentHD - 1`
- Right child → HD = `parentHD + 1`

---

## Approach

1. Use a **map** to store: hd → node value
(Only the first node for each HD is stored)
2. Use a **queue** for BFS that stores: (Node*, horizontal_distance)
3. Traverse the tree:
- If an HD is not already present in the map, insert it
4. Finally, iterate over the map from left to right to get the top view.

---

## Time & Space Complexity

- **Time Complexity:** `O(N log N)`
- `O(N)` for traversal
- `log N` for map insertions
- **Space Complexity:** `O(N)`
- Map + queue

---

## Complete C++ Code 

```cpp
#include <bits/stdc++.h>
using namespace std;

// Definition of Binary Tree Node
struct Node {
 int data;
 Node* left;
 Node* right;

 Node(int val) {
     data = val;
     left = right = NULL;
 }
};

// Function to get the top view of the binary tree
vector<int> topView(Node* root) {
 vector<int> ans;
 if (root == NULL)
     return ans;

 // Map to store first node at every horizontal distance
 map<int, int> topNode;

 // Queue stores pair of (node, horizontal distance)
 queue<pair<Node*, int>> q;
 q.push(make_pair(root, 0));

 while (!q.empty()) {
     pair<Node*, int> temp = q.front();
     q.pop();

     Node* frontNode = temp.first;
     int hd = temp.second;

     // If this HD is encountered first time
     if (topNode.find(hd) == topNode.end()) {
         topNode[hd] = frontNode->data;
     }

     if (frontNode->left)
         q.push(make_pair(frontNode->left, hd - 1));

     if (frontNode->right)
         q.push(make_pair(frontNode->right, hd + 1));
 }

 // Store result from map into answer vector
 for (auto it : topNode) {
     ans.push_back(it.second);
 }

 return ans;
}

int main() {
 /*
         1
       /   \
      2     3
     / \     \
    4   5     6
           /
          7

     Top View: 4 2 1 3 6
 */

 Node* root = new Node(1);
 root->left = new Node(2);
 root->right = new Node(3);
 root->left->left = new Node(4);
 root->left->right = new Node(5);
 root->right->right = new Node(6);
 root->right->right->left = new Node(7);

 vector<int> result = topView(root);

 cout << "Top View of Binary Tree: ";
 for (int val : result) {
     cout << val << " ";
 }

 return 0;
}



