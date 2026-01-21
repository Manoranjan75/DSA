# Construct BST From Preorder Traversal 

Given the **preorder traversal** of a Binary Search Tree (BST), construct the original BST.

Example preorder: [10, 5, 1, 7, 40, 50]

Your task: Rebuild the BST **without using inorder traversal**, using only the preorder array.

---

# Key Idea

### Why can we reconstruct a BST from preorder alone?

Because BST property ensures:
- Left subtree < root
- Right subtree > root

### Preorder structure: Root → Left Subtree → Right Subtree


We can reconstruct the BST **using value ranges**:

- For root = `pre[0]`,  
  left subtree values must lie in range `(-∞, root)`
  right subtree values lie in `(root, +∞)`

During recursion:
- Each next value must belong to the allowed range.
- If it does, it becomes part of this subtree.
- Otherwise, subtree ends.

This ensures we rebuild the BST exactly.

---

# Approach (Using Range Method)

For each value in preorder:

1. If value is **outside allowed range**, it cannot be part of this subtree → return.
2. Otherwise:
   - Create node
   - Recursively construct left subtree (range: `minVal` to `val`)
   - Recursively construct right subtree (range: `val` to `maxVal`)

We maintain an index `idx` (passed by reference) so that each value is processed once.

---

# Time & Space Complexity

| Operation | Complexity |
|----------|-------------|
| Build BST | O(N) |
| Extra Space (recursion) | O(H) = O(N) worst case |

The algorithm is **O(N)** because each value is used exactly once.

---

# Complete C++ Code 

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

Node* buildBST(vector<int>& preorder, int& idx, long long minVal, long long maxVal){
    // Base case
    if(idx >= preorder.size()){
        return NULL;
    }

    int val = preorder[idx];

    // Check if current value fits BST range
    if(val <= minVal || val >= maxVal){
        return NULL;
    }

    // Create node
    Node* root = new Node(val);
    idx++;

    // Build left subtree
    root->left = buildBST(preorder, idx, minVal, val);

    // Build right subtree
    root->right = buildBST(preorder, idx, val, maxVal);

    return root;
}

Node* bstFromPreorder(vector<int>& preorder){
    int idx = 0;
    return buildBST(preorder, idx, LLONG_MIN, LLONG_MAX);
}

