# Sum Tree 

## Problem Statement  
Given a **binary tree**, determine whether it is a **Sum Tree**.

### Definition  
A binary tree is called a **Sum Tree** if **for every non-leaf node**: node->data = sum of values in left subtree + sum of values in right subtree


Rules:
- An **empty tree** is a Sum Tree.
- A **leaf node** is also considered a Sum Tree.

---

## Example

    26
   /  \
 10    3
/ \     \
4  6     3


Explanation:
- Node 10 = 4 + 6
- Node 3  = 0 + 3
- Node 26 = 10 + 3  
✅ Hence, it is a Sum Tree.

---

## Approach (Postorder Traversal + Pair)

We solve this using **postorder traversal** (Left → Right → Root).

For each node, we return a `pair<int, int>`:
- `first`  → **sum of subtree**
- `second` → **isSumTree flag** (`1 = true`, `0 = false`)

### Logic

1. **Base Cases**
   - If node is `NULL` → return `{0, true}`
   - If node is a **leaf** → return `{node->data, true}`

2. **Recursive Step**
   - Get results from left and right subtrees.
   - Current node is a Sum Tree if:
     ```
     left.isSumTree &&
     right.isSumTree &&
     root->data == left.sum + right.sum
     ```
   - Total sum returned upward:
     ```
     root->data + left.sum + right.sum
     ```

This approach ensures:
- **O(N)** time (each node visited once)
- No repeated subtree sum calculations

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(H)`  
  (`H` = height of tree, due to recursion stack)

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

pair<int, int> checkSumTree(Node* root) {
    // Empty tree
    if (root == NULL)
        return {0, 1};   // {sum, isSumTree}

    // Leaf node
    if (root->left == NULL && root->right == NULL)
        return {root->data, 1};

    // Get left and right subtree info
    auto left = checkSumTree(root->left);
    auto right = checkSumTree(root->right);

    bool isSumTree = left.second &&
                     right.second &&
                     (root->data == left.first + right.first);

    int totalSum = root->data + left.first + right.first;

    return {totalSum, isSumTree};
}

bool isSumTree(Node* root) {
    return checkSumTree(root).second;
}

int main() {
    /*
            26
           /  \
         10    3
        / \     \
       4   6     3
    */

    Node* root = new Node(26);
    root->left = new Node(10);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(6);
    root->right->right = new Node(3);

    cout << isSumTree(root);   // Output: 1 (true)

    return 0;
}

