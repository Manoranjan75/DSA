# Construct Binary Tree from Preorder and Inorder Traversals 

You are given two arrays:
- **Inorder traversal** of a binary tree  
- **Preorder traversal** of the same binary tree  

Your task is to **reconstruct the original binary tree**.

### Traversal Rules
- **Preorder** → Root, Left, Right  
- **Inorder** → Left, Root, Right  

### Assumptions
- All node values are **unique**
- The given traversals represent a **valid binary tree**

---

## Core Idea

### Key Observations
1. The **first element of preorder** is always the **root** of the tree.
2. In inorder traversal:
   - Elements to the **left of root** form the **left subtree**
   - Elements to the **right of root** form the **right subtree**
3. Recursively repeat the same steps for left and right subtrees.

To optimize lookup of root position in inorder traversal, we use a **map**.

---

## Approach Breakdown

### Step 1: Create Inorder Index Mapping
- Store each value of inorder traversal with its index.
- This allows `O(1)` lookup for root positions.

### Step 2: Recursive Tree Construction
Use a recursive function that takes:
- Current preorder index
- Current inorder range (`start` to `end`)

For each recursive call:
1. Pick the current element from preorder as root.
2. Find its position in inorder using the map.
3. Recursively construct:
   - Left subtree from inorder `[start, position - 1]`
   - Right subtree from inorder `[position + 1, end]`

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`  
  (Each node processed once)
- **Space Complexity:** `O(N)`  
  (Map + recursion stack)

---

## Complete C++ Code

```cpp
#include<bits/stdc++.h>
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

// Create value -> index mapping for inorder
void createMapping(vector<int> &in, map<int, int> &nodeToIndex) {
    for (int i = 0; i < in.size(); i++) {
        nodeToIndex[in[i]] = i;
    }
}

Node* solve(vector<int> &in, vector<int> &pre, int &index,
            int inorderStart, int inorderEnd,
            map<int, int> &nodeToIndex) {

    // Base case
    if (index >= pre.size() || inorderStart > inorderEnd)
        return NULL;

    int element = pre[index++];
    Node* root = new Node(element);

    int position = nodeToIndex[element];

    // Recursive calls
    root->left = solve(in, pre, index,
                       inorderStart, position - 1,
                       nodeToIndex);

    root->right = solve(in, pre, index,
                        position + 1, inorderEnd,
                        nodeToIndex);

    return root;
}

Node* buildTree(vector<int> &in, vector<int> &pre) {
    int preOrderIndex = 0;
    map<int, int> nodeToIndex;

    createMapping(in, nodeToIndex);

    return solve(in, pre, preOrderIndex, 0, in.size() - 1, nodeToIndex);
}

// Utility function to verify using postorder traversal
void printPostorder(Node* root) {
    if (!root) return;
    printPostorder(root->left);
    printPostorder(root->right);
    cout << root->data << " ";
}

int main() {
    /*
        Inorder   : 4 2 5 1 6 3
        Preorder  : 1 2 4 5 3 6

        Tree:
                1
              /   \
             2     3
            / \   /
           4   5 6
    */

    vector<int> inorder  = {4, 2, 5, 1, 6, 3};
    vector<int> preorder = {1, 2, 4, 5, 3, 6};

    Node* root = buildTree(inorder, preorder);

    cout << "Postorder traversal of constructed tree: ";
    printPostorder(root);
    cout << endl;

    return 0;
}
