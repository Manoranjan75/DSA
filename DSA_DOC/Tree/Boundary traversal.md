# Boundary Traversal of a Binary Tree 

Given a **binary tree**, print its **boundary traversal** in an **anti-clockwise direction**, starting from the root.

### Boundary Traversal Order
1. **Root node**
2. **Left boundary** (excluding leaf nodes)
3. **All leaf nodes** (left to right)
4. **Right boundary** (excluding leaf nodes, printed bottom-up)

---

## Approach Breakdown

We split the traversal into **three independent parts**:

### 1. Left Boundary Traversal
- Traverse down the **left side** of the tree.
- **Exclude leaf nodes** to avoid duplication.
- Prefer `left` child; if absent, go to `right`.

### 2. Leaf Nodes Traversal
- Traverse the entire tree.
- Add nodes that have **no left and right child**.
- Do this for **both left and right subtrees**.

### 3. Right Boundary Traversal
- Traverse down the **right side** of the tree.
- **Exclude leaf nodes**.
- Prefer `right` child; if absent, go to `left`.
- Add nodes **after recursion** (to get bottom-up order).

---

## Why This Works

- Each node is visited **at most once**.
- Leaf nodes are handled separately to avoid duplication.
- Order strictly follows **anti-clockwise boundary traversal**.

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(H)`  
  (`H` = height of the tree due to recursion stack)

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

// Traverse left boundary (excluding leaf nodes)
void traverse_left(Node* root, vector<int> &ans){
    if(root == NULL || (root->left == NULL && root->right == NULL)){
        return;
    }

    ans.push_back(root->data);

    if(root->left != NULL){
        traverse_left(root->left, ans);
    }
    else{
        traverse_left(root->right, ans);
    }
}

// Traverse right boundary (excluding leaf nodes, bottom-up)
void traverse_right(Node* root, vector<int> &ans){
    if(root == NULL || (root->left == NULL && root->right == NULL)){
        return;
    }

    if(root->right != NULL){
        traverse_right(root->right, ans);
    }
    else{
        traverse_right(root->left, ans);
    }

    ans.push_back(root->data);
}

// Traverse all leaf nodes
void traverse_leaf(Node* root, vector<int> &ans){
    if(root == NULL){
        return;
    }

    if(root->left == NULL && root->right == NULL){
        ans.push_back(root->data);
    }

    traverse_leaf(root->left, ans);
    traverse_leaf(root->right, ans);
}

// Boundary traversal function
vector<int> Boundary_traversal(Node* root){
    vector<int> ans;
    if(root == NULL){
        return ans;
    }

    // Root
    ans.push_back(root->data);

    // Left boundary
    traverse_left(root->left, ans);

    // Leaf nodes
    traverse_leaf(root->left, ans);
    traverse_leaf(root->right, ans);

    // Right boundary
    traverse_right(root->right, ans);

    return ans;
}

int main(){
    /*
            1
          /   \
         2     3
        / \     \
       4   5     6
    */

    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);

    vector<int> result = Boundary_traversal(root);

    cout << "Boundary Traversal: ";
    for(int x : result){
        cout << x << " ";
    }

    return 0;
}
