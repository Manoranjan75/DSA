# Zig-Zag (Spiral) 

Given a **binary tree**, print its **level order traversal** such that the direction alternates at every level:
- Level 0 → **Left to Right**
- Level 1 → **Right to Left**
- Level 2 → **Left to Right**, and so on.

This traversal is also known as **Zig-Zag** or **Spiral** traversal.

---

## Example

For the tree:
1 -> (2, 3),  2 -> (4, 5), 3 -> (NULL, 6)

**Output:**
1
3 2
4 5 6


---

## Approach (Level Order Traversal using Queue)

We perform a standard **BFS (level order traversal)** with a small twist:

### Key Idea
- Use a **queue** to process nodes level by level.
- Maintain a boolean flag `leftToRight` to control the direction at each level.
- For each level:
  - Create a vector `level` of size equal to the number of nodes at that level.
  - Decide the index to insert the current node’s value:
    ```
    index = leftToRight ? i : (size - 1 - i)
    ```
- Flip the direction after completing each level.

This avoids reversing arrays and keeps the solution efficient.

---

## Time & Space Complexity

- **Time Complexity:** `O(N)`  
  (each node is visited exactly once)
- **Space Complexity:** `O(N)`  
  (queue + result storage)

---

## Complete C++ Code
```cpp
#include<bits/stdc++.h>
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

vector<vector<int>> zigzagLevelOrder(Node* root) {
    vector<vector<int>> res;
    if (root == NULL) return res;

    queue<Node*> q;
    q.push(root);

    bool leftToRight = true;

    while (!q.empty()) {
        int size = q.size();
        vector<int> level(size);

        for (int i = 0; i < size; i++) {
            Node* curr = q.front();
            q.pop();

            // Decide index based on direction
            int index = leftToRight ? i : (size - 1 - i);
            level[index] = curr->data;

            if (curr->left) q.push(curr->left);
            if (curr->right) q.push(curr->right);
        }

        res.push_back(level);
        leftToRight = !leftToRight;  // flip direction
    }

    return res;
}

int main() {

    /*
            1
           / \
          2   3
         / \   \
        4   5   6
    */

    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);

    vector<vector<int>> ans = zigzagLevelOrder(root);

    cout << "Zig-Zag Traversal:\n";
    for (auto &level : ans) {
        for (int val : level) {
            cout << val << " ";
        }
        cout << endl;
    }

    return 0;
}
