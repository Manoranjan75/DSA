# Construct a BST From Inorder Traversal 

## Problem Statement
Given the **inorder traversal** of a Binary Search Tree (BST), construct the BST.

### Important Observation  
The inorder traversal of a BST is **always sorted**.  
However, **multiple BSTs** can yield the same inorder traversal.

Therefore, inorder alone **cannot** reconstruct the original BST uniquely.

### Standard Solution  
To construct a valid BST from inorder, we usually create a **Balanced BST** (minimum height BST) by choosing the **middle element as root**.

---

## Why Middle Element?
Choosing the middle:
- Ensures **balanced height**  
- Ensures **log N depth**
- Provides optimal search performance

If you choose left-most or right-most first, the tree becomes skewed (like a linked list).

---

## Approach

Given a sorted inorder array: [1, 2, 3, 4, 5, 6, 7]




### Steps
1. Pick middle element → root  
2. Recursively build left subtree from left half  
3. Recursively build right subtree from right half  
4. Return root

---

## Time & Space Complexity

| Operation | Complexity |
|----------|-------------|
| Build BST | O(N) |
| Space (recursion) | O(log N) (balanced) |

---

## Full Working Code (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

// Build BST from inorder (sorted array)
Node* buildFromInorder(vector<int> &in, int start, int end) {
    if (start > end)
        return NULL;

    int mid = start + (end - start) / 2;

    Node* root = new Node(in[mid]);

    root->left = buildFromInorder(in, start, mid - 1);
    root->right = buildFromInorder(in, mid + 1, end);

    return root;
}

// Inorder print for verification
void printInorder(Node* root) {
    if (!root) return;
    printInorder(root->left);
    cout << root->data << " ";
    printInorder(root->right);
}

int main() {

    /*
        Given inorder (sorted):
        1 2 3 4 5 6 7

        Balanced BST:

                4
              /   \
             2     6
            / \   / \
           1   3 5   7
    */

    vector<int> inorder = {1, 2, 3, 4, 5, 6, 7};

    Node* root = buildFromInorder(inorder, 0, inorder.size() - 1);

    cout << "Inorder of Constructed BST: ";
    printInorder(root);

    return 0;
}