# Left View and Right View of a Binary Tree

Given a **binary tree**, print:
1. **Left View** of the tree  
2. **Right View** of the tree  

### Definitions
- **Left View**: Nodes visible when the tree is viewed from the **left side**.
  - For each level, the **first node** encountered is part of the left view.
- **Right View**: Nodes visible when the tree is viewed from the **right side**.
  - For each level, the **last node** encountered is part of the right view.

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

**Left View** :  1247

**Right View** : 1367


---

## Core Idea (Level Order Traversal)

Both views are solved using **Level Order Traversal (BFS)**.

### Key Observations
- Traverse the tree **level by level** using a queue.
- At each level:
  - **Left View** → take the **first node** (`i == 0`)
  - **Right View** → take the **last node** (`i == size - 1`)

This guarantees that only visible nodes from each side are selected.

---

## Approach

### Left View Algorithm
1. Use a queue and push the root.
2. For each level:
   - Traverse all nodes at that level.
   - Store the **first node’s data**.
3. Push left child first, then right child.

### Right View Algorithm
1. Use a queue and push the root.
2. For each level:
   - Traverse all nodes at that level.
   - Store the **last node’s data**.
3. Push left child first, then right child.

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`  
  (Each node is visited once)
- **Space Complexity:** `O(N)`  
  (Queue in worst case)

---

## Complete C++ Code 

```cpp
#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node definition
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

// ---------------- LEFT VIEW ----------------
vector<int> leftView(Node* root) {
    vector<int> ans;
    if (root == NULL) return ans;

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();

        for (int i = 0; i < size; i++) {
            Node* curr = q.front();
            q.pop();

            // First node of each level
            if (i == 0)
                ans.push_back(curr->data);

            if (curr->left)
                q.push(curr->left);
            if (curr->right)
                q.push(curr->right);
        }
    }
    return ans;
}

// ---------------- RIGHT VIEW ----------------
vector<int> rightView(Node* root) {
    vector<int> ans;
    if (root == NULL) return ans;

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();

        for (int i = 0; i < size; i++) {
            Node* curr = q.front();
            q.pop();

            // Last node of each level
            if (i == size - 1)
                ans.push_back(curr->data);

            if (curr->left)
                q.push(curr->left);
            if (curr->right)
                q.push(curr->right);
        }
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

        Left View  : 1 2 4 7
        Right View : 1 3 6 7
    */

    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);
    root->right->right->left = new Node(7);

    vector<int> lv = leftView(root);
    vector<int> rv = rightView(root);

    cout << "Left View: ";
    for (int x : lv)
        cout << x << " ";
    cout << endl;

    cout << "Right View: ";
    for (int x : rv)
        cout << x << " ";
    cout << endl;

    return 0;
}


