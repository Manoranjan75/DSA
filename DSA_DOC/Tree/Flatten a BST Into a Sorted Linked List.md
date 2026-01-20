# Flatten a BST Into a Sorted Linked List 

Given a **Binary Search Tree (BST)**, flatten it into a **sorted linked list**.

The linked list should be:
- **Right-skewed** (each node’s right pointer points to the next node)
- **Left pointers must be null**
- Nodes should appear in **increasing order**

---

## Example

### Input BST:
```
        8
      /   \
     3     10
    / \      \
   1   6      14
      / \     /
     4   7   13


```
### Output Linked List: 1 -> 3 -> 4 -> 6 -> 7 -> 8 -> 10 -> 13 -> 14 -> NULL



---

# Approach

### Step 1: Inorder Traversal  
Since BST inorder traversal gives **sorted order**, collect all nodes in a vector.

### Step 2: Re-link Nodes  
Convert vector into a linked list:
- `left = NULL`
- `right = next node`

### Result  
A fully **flattened** BST in sorted order using the existing tree nodes.

---

# Time & Space Complexity

| Operation | Complexity |
|----------|-------------|
| Inorder Traversal | O(N) |
| Re-linking nodes | O(N) |
| Extra space (vector) | O(N) |

Total: **O(N)** time and **O(N)** space.

---

# C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Node{
public:
    int data;
    Node* left;
    Node* right;

    Node(int data){
        this->data = data;
        left = right = NULL;
    }
};

// Step 1: Inorder traversal to store nodes
void inorder(Node* root, vector<Node*>& nodes){
    if(root == NULL) return;

    inorder(root->left, nodes);
    nodes.push_back(root);
    inorder(root->right, nodes);
}

// Step 2: Relink nodes to form sorted linked list (right-skewed)
Node* flattenBST(Node* root){
    if(root == NULL) return NULL;

    vector<Node*> nodes;
    inorder(root, nodes);

    int n = nodes.size();
    for(int i = 0; i < n - 1; i++){
        nodes[i]->left = NULL;
        nodes[i]->right = nodes[i + 1];
    }

    // Last node
    nodes[n - 1]->left = NULL;
    nodes[n - 1]->right = NULL;

    // Head of linked list
    return nodes[0];
}
