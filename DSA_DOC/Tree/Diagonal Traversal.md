# Diagonal Traversal of a Binary Tree — Single Page Notes + Code

## Problem Statement  
Given a **binary tree**, print its **diagonal traversal**.

### Definition  
In diagonal traversal:
- All nodes having the same **diagonal distance** from the root are printed together.
- Convention used:
  - **Right child** stays on the **same diagonal**
  - **Left child** moves to the **next diagonal**

Traversal is printed **diagonal by diagonal**, starting from the root’s diagonal.

---

## Example

For the tree:

```
        1
      /   \
     2     3
    / \     \
   4   5     6
          /
         7

```


### Diagonals
- Diagonal 0 → `1, 3, 6`
- Diagonal 1 → `2, 5, 7`
- Diagonal 2 → `4`

**Output:** 1 3 6 2 5 7 4


---

## Core Idea (BFS + Diagonal Index)

We use **level-order traversal (BFS)** with a twist:
- Maintain a **diagonal number** for each node.
- Use a **map** to group nodes belonging to the same diagonal.

### Diagonal Rules
- Root has diagonal `0`
- Left child → `diag + 1`
- Right child → `diag`

---

## Approach

1. Use a queue storing: (Node*, diagonal)
2. Use a map: diagonal → list of node values
3. Start with `(root, 0)` in the queue.
4. For each node:
- Insert its value into `diagMap[diagonal]`
- Push left child with `diagonal + 1`
- Push right child with same `diagonal`
5. Finally, traverse the map in increasing diagonal order and collect results.

---

## Time & Space Complexity

- **Time Complexity:** `O(N log N)`
- `N` nodes traversal
- `log N` for map insertion
- **Space Complexity:** `O(N)`
- Queue + map storage

---

## Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct Node {
 int data;
 Node* left;
 Node* right;

 Node(int val) {
     data = val;
     left = right = NULL;
 }
};

// Function for Diagonal Traversal
vector<int> diagonalTraversal(Node* root) {
 vector<int> ans;
 if (root == NULL)
     return ans;

 // Map: diagonal number -> list of nodes
 map<int, vector<int>> diagMap;

 // Queue stores (node, diagonal)
 queue<pair<Node*, int>> q;
 q.push({root, 0});

 while (!q.empty()) {
     auto temp = q.front();
     q.pop();

     Node* curr = temp.first;
     int diag = temp.second;

     diagMap[diag].push_back(curr->data);

     // Left child goes to next diagonal
     if (curr->left)
         q.push({curr->left, diag + 1});

     // Right child stays on same diagonal
     if (curr->right)
         q.push({curr->right, diag});
 }

 // Store result diagonal-wise
 for (auto &it : diagMap) {
     for (int val : it.second)
         ans.push_back(val);
 }

 return ans;
}

// ---------------- DRIVER CODE ----------------
int main() {
 /*
         1
       /   \
      2     3
     / \     \
    4   5     6
           /
          7

     Diagonal Traversal:
     1 3 6 2 5 7 4
 */

 Node* root = new Node(1);
 root->left = new Node(2);
 root->right = new Node(3);
 root->left->left = new Node(4);
 root->left->right = new Node(5);
 root->right->right = new Node(6);
 root->right->right->left = new Node(7);

 vector<int> result = diagonalTraversal(root);

 cout << "Diagonal Traversal: ";
 for (int x : result)
     cout << x << " ";
 cout << endl;

 return 0;
}

