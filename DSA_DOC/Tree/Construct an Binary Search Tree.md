# Construct a Binary Search Tree (BST) 


Construct a **Binary Search Tree (BST)** by inserting elements one by one from user input and then print its **Inorder Traversal**.

### Input Rule
- Elements are inserted **until `-1` is encountered**
- `-1` indicates end of input
- All other values are valid BST nodes

---

## Binary Search Tree (BST) Property

For every node:
- Left subtree contains values **less than** the node
- Right subtree contains values **greater than or equal to** the node

This property must be maintained during insertion.

---

## Core Idea

### BST Insertion (Recursive)
To insert a value `data`:
1. If the current root is `NULL`, create a new node.
2. If `data < root->data`, insert into the **left subtree**.
3. Otherwise, insert into the **right subtree**.
4. Return the root after insertion.

---

## Why Inorder Traversal?

In a BST:
> **Inorder traversal always prints elements in sorted order.**

So it is commonly used to verify whether a tree is a valid BST.

---

## Approach

1. Read values from input until `-1`.
2. Insert each value into the BST using recursion.
3. Perform **Inorder Traversal** to print the BST.

---

## Time & Space Complexity

### Insertion
- **Average Case:** `O(log N)`
- **Worst Case (skewed tree):** `O(N)`

### Traversal
- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(H)`  
  (`H` = height of BST, due to recursion stack)

---

## Complete C++ Code 

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
public:
    int data;
    Node* left;
    Node* right;

    Node(int data){
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Insert a node into BST
Node* solve(Node* root, int data){
    // Base case
    if(root == NULL){
        root = new Node(data);
        return root;
    }

    if(data < root->data){
        root->left = solve(root->left, data);
    }
    else{
        root->right = solve(root->right, data);
    }

    return root;
}

// Build BST from input
void bst(Node* &root){
    int data;
    cout << "Enter the root data: ";
    cin >> data;

    while(data != -1){
        root = solve(root, data);
        cin >> data;
    }
}

// Inorder Traversal
void inOrder(Node* root){
    if(root == NULL){
        return;
    }
    inOrder(root->left);
    cout << root->data << " ";
    inOrder(root->right);
}

int main(){
    Node* root = NULL;

    bst(root);

    cout << "Inorder Traversal of BST: ";
    inOrder(root);

    return 0;
}
