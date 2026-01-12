# Morris Traversal (Inorder Traversal without Recursion & Stack)


Perform **Inorder Traversal** of a binary tree **without using recursion and without using an explicit stack**.

This traversal must run in:
- **O(N) time**
- **O(1) extra space**

This is achieved using **Morris Traversal**.

---

## What is Morris Traversal?

**Morris Traversal** is a clever tree traversal technique that:
- Temporarily modifies the tree structure
- Uses **threaded binary tree concept**
- Restores the original tree after traversal

It allows inorder traversal using **constant space**.

---

## Inorder Traversal Reminder
Left → Root → Right


---

## Core Idea

For each node:
1. If the **left child is NULL**:
   - Visit the node
   - Move to the right child
2. If the **left child exists**:
   - Find the **inorder predecessor** (rightmost node in left subtree)
   - If predecessor’s right is NULL:
     - Make a temporary link (thread) to current node
     - Move to left child
   - If predecessor’s right already points to current:
     - Remove the thread
     - Visit current node
     - Move to right child

This ensures every node is visited exactly **twice at most**.

---

## Why This Works

- Threads allow us to return to a node after finishing its left subtree
- No recursion stack or explicit stack is required
- Tree structure is restored after traversal

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)` (no extra memory)

---

## Complete C++ Code 

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

void morrisTraversal(Node* root) {
    Node* current = root;

    while (current != NULL) {

        // Case 1: left does not exist
        if (current->left == NULL) {
            cout << current->data << " ";   // visit
            current = current->right;
        }
        else {
            // Find inorder predecessor
            Node* predecessor = current->left;
            while (predecessor->right != NULL &&
                   predecessor->right != current) {
                predecessor = predecessor->right;
            }

            // If right of predecessor is NULL, create thread
            if (predecessor->right == NULL) {
                predecessor->right = current;  // temporary link
                current = current->left;
            }
            // Thread already exists
            else {
                predecessor->right = NULL;     // remove thread
                cout << current->data << " ";  // visit
                current = current->right;
            }
        }
    }
}

int main() {
    /*
            1
           / \
          2   3
         / \
        4   5
    */

    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    morrisTraversal(root);
    return 0;
}
