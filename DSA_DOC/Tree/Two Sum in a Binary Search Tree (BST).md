# Two Sum in a Binary Search Tree (BST) 

Given a **Binary Search Tree (BST)** and a **target sum**, determine whether there exist **two nodes** in the BST such that: node1->data + node2->data = target


Return:
- `true` → if such a pair exists  
- `false` → otherwise  

---

## Key Idea

### Why This Works in BST  
A BST’s **inorder traversal** produces a **sorted array**.

Example:

```
         8
       /   \
      3    10
     / \
    16  14

Inorder → [1, 3, 6, 8, 10, 14]

```


Once we have a *sorted array*, the problem becomes the **classic Two-Pointer Two Sum** problem.

---

## Steps

### Step 1: Inorder Traversal  
Store BST elements in a sorted vector.

### Step 2: Two Pointer Method  
Use indices: i = 0 , j = arr.size() - 1


While `i < j`:
- If `arr[i] + arr[j] == target` → **found**
- If sum < target → move `i++`
- If sum > target → move `j--`

---

## Time & Space Complexity

| Operation               | Complexity |
|------------------------|------------|
| Inorder traversal       | O(N)       |
| Two-pointer search      | O(N)       |
| **Total Time**          | O(N)       |
| Extra space (vector)    | O(N)       |

---

# C++

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

// Inorder traversal to store sorted elements
void inorder(Node* root, vector<int>& arr){
    if(root == NULL) return;

    inorder(root->left, arr);
    arr.push_back(root->data);
    inorder(root->right, arr);
}

// Two Sum in BST
bool twoSumBST(Node* root, int target){
    vector<int> arr;
    inorder(root, arr);   // O(N)

    int i = 0, j = arr.size() - 1;

    while(i < j){
        int sum = arr[i] + arr[j];

        if(sum == target){
            return true;
        }
        else if(sum < target){
            i++;
        }
        else{
            j--;
        }
    }
    return false;
}


