# 🌳 Binary Tree Key Concepts  

---

## 1. Height of a Binary Tree  

**What it means:**  
The height of a tree is the maximum number of nodes along the path from the root node to the deepest leaf node.  

**Approach used:**  
- If the tree is empty, the height is `0`.  
- Otherwise, recursively calculate the height of the left and right subtrees and take the maximum, then add `1` for the current node.  

**Time Complexity:**  
- `O(N)` where `N = number of nodes`.  

**Importance:**  
- Height is used in many tree-based problems like balance checking, diameter, and tree traversal limits.  

---

## 2. Diameter of a Binary Tree  

**What it means:**  
The diameter of a tree is the length of the longest path between any two nodes in the tree.  

**Two Approaches:**  
1. **Brute Force (O(N²))**:  
   - For each node, calculate the height of left and right subtrees.  
   - Take the maximum diameter among them.  

2. **Optimized (O(N))**:  
   - Use recursion to return both height and diameter in one pass, avoiding repeated calculations.  

**Why it matters:**  
- It’s a classic interview problem as it combines the concepts of recursion, height, and traversal efficiency.  

---

## 3. Balanced Binary Tree Check  

**What it means:**  
A binary tree is balanced if the height difference between its left and right subtrees is not more than `1` for every node.  

**Optimized Approach:**  
- Use a recursive function that returns both:  
  - a boolean (`is balanced?`)  
  - and the height of the subtree.  
- At each node:  
  - Check if the left and right subtrees are balanced.  
  - Ensure their height difference ≤ `1`.  

**Time Complexity:**  
- `O(N)` because each node is visited once.  

**Why it matters:**  
- Balanced trees (like AVL, Red-Black Trees) ensure efficient operations like search, insert, and delete.  

---


# 🌳 Binary Tree Implementation in C++  


##  Code  

```cpp
#include <bits/stdc++.h>
using namespace std;

class Node { // Class to represent a Node for the Tree.
public:
    int data;
    Node* left;
    Node* right;

    Node(int data) {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Build tree from user input
Node* BuildTree(Node* root) {
    int data;
    cout << "Enter the data: ";
    cin >> data;

    if (data == -1) {
        return NULL;
    }

    root = new Node(data);

    cout << "Enter data to the left of " << data << endl;
    root->left = BuildTree(root->left);

    cout << "Enter data to the right of " << data << endl;
    root->right = BuildTree(root->right);

    return root;
}

// Level Order Traversal
void Level_Order(Node* root) {
    if (root == NULL) {
        return;
    }

    queue<Node*> qt;
    qt.push(root);
    qt.push(NULL);

    while (!qt.empty()) {
        Node* temp = qt.front();
        qt.pop();

        if (temp == NULL) {
            cout << endl;
            if (!qt.empty()) {
                qt.push(NULL);
            }
        } else {
            cout << temp->data << " ";
            if (temp->left) {
                qt.push(temp->left);
            }
            if (temp->right) {
                qt.push(temp->right);
            }
        }
    }
}

// Height of Binary Tree
int bth(Node* root) {
    if (root == NULL) {
        return 0;
    }

    int left = bth(root->left);
    int right = bth(root->right);

    int height = max(left, right) + 1;

    return height;
}

// Brute force diameter O(N^2)
int diameterBrute(Node* root) {
    if (root == NULL) {
        return 0;
    }

    int opt_1 = diameterBrute(root->left);
    int opt_2 = diameterBrute(root->right);
    int opt_3 = bth(root->left) + bth(root->right) + 1;

    int ans = max(opt_3, max(opt_1, opt_2));

    return ans;
}

// Optimized O(N) diameter
pair<int, int> diameterFast(Node* root) {
    if (root == NULL) {
        return {0, 0}; // {diameter, height}
    }

    auto left = diameterFast(root->left);
    auto right = diameterFast(root->right);

    int leftDiameter = left.first;
    int rightDiameter = right.first;
    int throughRoot = left.second + right.second + 1;

    int diameter = max(throughRoot, max(leftDiameter, rightDiameter));
    int height = max(left.second, right.second) + 1;

    return {diameter, height};
}

int diameter(Node* root) {
    return diameterFast(root).first;
}

// Check if tree is balanced
pair<bool, int> isBalancedFast(Node* root) {
    if (root == NULL) {
        return {true, 0};
    }

    auto left = isBalancedFast(root->left);
    auto right = isBalancedFast(root->right);

    bool leftAns = left.first;
    bool rightAns = right.first;

    bool diff = abs(left.second - right.second) <= 1;

    pair<bool, int> ans;
    ans.second = max(left.second, right.second) + 1;

    if (leftAns && rightAns && diff) {
        ans.first = true;
    } else {
        ans.first = false;
    }
    return ans;
}

bool isBalanced(Node* root) {
    return isBalancedFast(root).first;
}

int main() {
    // SAMPLE TREE (HARDCODED)
    // Construct this tree:
    //          1
    //        /   \
    //       2     3
    //      / \
    //     4   5
    //
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    cout << "Level Order Traversal: " << endl;
    Level_Order(root);
    cout << endl;

    cout << "Height of the tree: " << bth(root) << endl;

    cout << "Diameter (Brute Force O(N^2)): " << diameterBrute(root) << endl;

    cout << "Diameter (Optimized O(N)): " << diameter(root) << endl;

    cout << "Is Balanced: " << (isBalanced(root) ? "Yes" : "No") << endl;

    return 0;
}

