#  Lowest Common Ancestor (LCA) in a Binary Tree (C++)

##  Problem Statement

Given the root of a binary tree and two nodes `p` and `q` in the tree, return their **Lowest Common Ancestor (LCA)**.

Definition: The lowest common ancestor of two nodes `p` and `q` is the lowest node in the tree that has both `p` and `q` as descendants (we allow a node to be a descendant of itself).

---

##  Example

Consider the tree:
    3
   / \
  5   1
 / \ / \
6  2 0  8
  / \
 7   4



- Input: `p = 5`, `q = 1` → Output: `3`  
- Input: `p = 6`, `q = 4` → Output: `5` (since 5 is ancestor of 6 and 4)

---

## ⚙️ Idea / Approach (Recursive)

Perform a DFS from the root:

1. If current node is `nullptr`, return `nullptr`.
2. If current node is `p` or `q`, return current node (found one target).
3. Recursively search left and right subtrees:
   - `left = dfs(root->left)`
   - `right = dfs(root->right)`
4. Combine results:
   - If both `left` and `right` are non-null → current node is LCA, return `root`.
   - If one is non-null → propagate the non-null result upward.
   - If both null → return `nullptr`.

This works because once both targets are found in separate subtrees of a node, that node is the lowest ancestor covering both.

---

##  C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Recursive LCA for a binary tree (not a BST)
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root) return nullptr;
    if (root == p || root == q) return root; // found one target

    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);

    if (left && right) return root;      // p and q found in different subtrees
    return left ? left : right;          // propagate non-null child or null
}

// Helper: build a tree from level-order vector where -1 means null
TreeNode* buildTree(const vector<int>& vals) {
    if (vals.empty() || vals[0] == -1) return nullptr;
    TreeNode* root = new TreeNode(vals[0]);
    queue<TreeNode*> q;
    q.push(root);
    size_t i = 1;
    while (i < vals.size()) {
        TreeNode* node = q.front(); q.pop();
        // left child
        if (i < vals.size() && vals[i] != -1) {
            node->left = new TreeNode(vals[i]);
            q.push(node->left);
        }
        i++;
        // right child
        if (i < vals.size() && vals[i] != -1) {
            node->right = new TreeNode(vals[i]);
            q.push(node->right);
        }
        i++;
    }
    return root;
}

// Helper: find node by value (assumes unique values)
TreeNode* findNode(TreeNode* root, int val) {
    if (!root) return nullptr;
    if (root->val == val) return root;
    TreeNode* left = findNode(root->left, val);
    if (left) return left;
    return findNode(root->right, val);
}

int main() {
    // Build sample tree using level-order with -1 for nulls:
    // Example: [3,5,1,6,2,0,8,-1,-1,7,4]
    vector<int> vals = {3,5,1,6,2,0,8,-1,-1,7,4};
    TreeNode* root = buildTree(vals);

    TreeNode* p = findNode(root, 5);
    TreeNode* q = findNode(root, 1);
    TreeNode* lca = lowestCommonAncestor(root, p, q);
    if (lca) cout << "LCA of 5 and 1: " << lca->val << '\n';

    p = findNode(root, 6);
    q = findNode(root, 4);
    lca = lowestCommonAncestor(root, p, q);
    if (lca) cout << "LCA of 6 and 4: " << lca->val << '\n';

    // Clean up omitted for brevity
    return 0;
}

