# Sum of Nodes on the Longest Root-to-Leaf Path 

Given a **binary tree**, find the **sum of nodes on the longest path from root to any leaf**.

If there are **multiple paths with the same maximum length**, return the **maximum sum among them**.

---

## Example

For the tree:
```
        4
       / \
      2   5
     / \   \
    7   1   2
       /
      6

```

- Longest root-to-leaf path: 4 → 2 → 1 → 6
- Length = 4  
- Sum = `4 + 2 + 1 + 6 = 13`

**Output:** 13


---

## Core Idea (DFS + Backtracking)

We perform a **Depth-First Search (DFS)** while tracking:
- Current path **length**
- Current path **sum**

At every **leaf node**, we:
1. Compare the current path length with the maximum length seen so far.
2. Update the maximum sum accordingly.

---

## Approach

### Variables Used
- `currLen` → current path length
- `currSum` → sum of current path
- `maxLen` → maximum path length found so far
- `maxSum` → maximum sum corresponding to `maxLen`

### Steps
1. Start DFS from the root with `currLen = 0` and `currSum = 0`.
2. At each node:
   - Increment `currLen`
   - Add node’s data to `currSum`
3. If a **leaf node** is reached:
   - If `currLen > maxLen`, update both `maxLen` and `maxSum`
   - If `currLen == maxLen`, update `maxSum` with the maximum sum
4. Continue DFS for left and right children.

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`  
  (Each node visited once)
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

// Helper DFS function
void solve(Node* root, int currLen, int currSum,
           int &maxLen, int &maxSum) {

    if (root == NULL)
        return;

    currLen++;
    currSum += root->data;

    // If leaf node
    if (root->left == NULL && root->right == NULL) {
        if (currLen > maxLen) {
            maxLen = currLen;
            maxSum = currSum;
        }
        else if (currLen == maxLen) {
            maxSum = max(maxSum, currSum);
        }
        return;
    }

    solve(root->left, currLen, currSum, maxLen, maxSum);
    solve(root->right, currLen, currSum, maxLen, maxSum);
}

// Function to return sum of longest path
int sumOfLongRootToLeafPath(Node* root) {
    int maxLen = 0;
    int maxSum = 0;

    solve(root, 0, 0, maxLen, maxSum);
    return maxSum;
}

int main() {
    /*
            4
           / \
          2   5
         / \   \
        7   1   2
           /
          6

    Longest path: 4 → 2 → 1 → 6
    Sum = 13
    */

    Node* root = new Node(4);
    root->left = new Node(2);
    root->right = new Node(5);
    root->left->left = new Node(7);
    root->left->right = new Node(1);
    root->left->right->left = new Node(6);
    root->right->right = new Node(2);

    cout << "Sum of longest root-to-leaf path: "
         << sumOfLongRootToLeafPath(root) << endl;

    return 0;
}
