# Maximum Sum of Non-Adjacent Nodes in a Binary Tree (Tree DP)

## Problem Statement  
Given a **binary tree**, find the **maximum sum of node values** such that **no two selected nodes are directly connected** (i.e., no parent and child are both included).

This is the **tree version of the “Maximum Sum of Non-Adjacent Elements”** (similar to House Robber, but on trees).

---

## Example

For the tree:
```
            10
           /  \
          1    2
         / \    \
        3   4    5

```

Valid selection (no adjacent nodes): 10 + 3 + 4 + 5 = 22


**Output:** 22

---

## Core Idea (Tree DP)

For every node, we calculate **two values**: pair<int,int> = {include, exclude}



### Meaning
- `include` → Maximum sum **including the current node**
- `exclude` → Maximum sum **excluding the current node**

---

## Recurrence Relation

For a given node `root`:

### 1. Include current node
If we include `root`, we **cannot include its children**: include = root->data + left.exclude + right.exclude



### 2. Exclude current node
If we exclude `root`, we can **choose max of include/exclude** from children: exclude = max(left.include, left.exclude) + max(right.include, right.exclude)


---

## Base Case

If `root == NULL`: {0, 0}


---

## Final Answer

At the root: max(include, exclude)

---

## Why This Works

- Ensures **no adjacent nodes** are selected
- Each node is processed **once**
- Avoids recomputation using **postorder traversal**

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(H)`  
  (`H` = height of tree due to recursion stack)

---

## Complete C++ Code 

```cpp
#include <bits/stdc++.h>
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

pair<int, int> solve(Node* root) {
    // Base case
    if (root == NULL) {
        return make_pair(0, 0);
    }

    pair<int, int> left = solve(root->left);
    pair<int, int> right = solve(root->right);

    pair<int, int> res;

    // Include current node
    res.first = root->data + left.second + right.second;

    // Exclude current node
    res.second = max(left.first, left.second) +
                 max(right.first, right.second);

    return res;
}

int getMaxSum(Node* root) {
    pair<int, int> ans = solve(root);
    return max(ans.first, ans.second);
}

int main() {
    /*
                10
               /  \
              1    2
             / \    \
            3   4    5

        Maximum Non-Adjacent Sum = 10 + 3 + 4 + 5 = 22
    */

    Node* root = new Node(10);
    root->left = new Node(1);
    root->right = new Node(2);

    root->left->left = new Node(3);
    root->left->right = new Node(4);
    root->right->right = new Node(5);

    cout << "Maximum Non-Adjacent Nodes Sum: "
         << getMaxSum(root) << endl;

    return 0;
}
