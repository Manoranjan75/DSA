# Find the Middle of a Linked List (C++)

## Problem Statement
Given the head of a singly linked list, find the node that lies in the **middle** of the list.

If the number of nodes is even, return the **second middle** node.

Example:
List: 1 → 2 → 3 → 4 → 5  
Output: 3

List: 1 → 2 → 3 → 4  
Output: 3 (second middle)

---

## Approach (Fast–Slow Pointer)
Use two pointers:

- `slow` moves **1 step**
- `fast` moves **2 steps**

When `fast` reaches the end:
- `slow` will be at the **middle node**.

This works because `fast` runs twice as fast as `slow`.

---
| Type  | Complexity |
| ----- | ---------- |
| Time  | O(n)       |
| Space | O(1)       |


---

## C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int val) {
        data = val;
        next = NULL;
    }
};

// Function to find middle node
Node* middleNode(Node* head) {
    Node* slow = head;
    Node* fast = head;

    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;  // middle node
}

// Utility function to print list
void printList(Node* head) {
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    cout << "Linked List: ";
    printList(head);

    Node* mid = middleNode(head);
    cout << "Middle Node: " << mid->data << endl;

    return 0;
}
