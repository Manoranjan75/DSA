# Circular Singly Linked List

## Problem Statement

Implement a circular singly linked list supporting:

- Insert at head
- Insert at any position (1-based index)
- Delete at any position (1-based index)
- Display the list (showing it cycles back to head)

Behavioral details:
- The list is circular: the `next` pointer of the last node points back to the `head`.
- Inserting at position `1` or inserting into an empty list should place the new node at the head.
- If an insertion position is beyond the current list length, the new node is appended at the end.
- Deletion at position `1` should correctly handle single-node lists and multi-node lists by updating the head and last node's `next`.
- Deletions at out-of-range positions are ignored.

---

## Approach / Design

- **Node structure**: each node stores an integer `data` and a `next` pointer.
- **InsertAtHead**:
  - If the list is empty: create node, set its `next` to itself, and set `head` to this node.
  - Otherwise: traverse to last node (node whose `next` points to `head`), link the new node before current head, update last's `next` to the new node, and set new node as `head`.
- **InsertAtAny**:
  - If `position <= 1` or list is empty: delegate to `InsertAtHead`.
  - Otherwise: move to node at `position-1` (or to last node if position is beyond length), insert new node after current node by adjusting `next` pointers.
- **deletionAtAny**:
  - If list is empty: do nothing.
  - If `position == 1`:
    - If single node: delete and set `head = NULL`.
    - Else: find last node, move `head` to `head->next`, set last's `next` to new head, delete old head.
  - If `position > 1`: move to node at `position-1` (or stop earlier if reach last), if `curr->next == head` then position out of range — do nothing; otherwise unlink and delete the node at `curr->next`.
- **display**:
  - If head is `NULL`, print "List is empty".
  - Otherwise traverse from head using a `do-while` loop until we come back to head and print node values in order.

All pointer updates ensure the circular property is preserved.

---

## Time & Space Complexity

- **InsertAtHead**: `O(n)` because we must find the last node (unless we maintained a tail pointer).  
- **InsertAtAny**: `O(min(n, position))` → worst-case `O(n)` to reach insertion point.
- **deletionAtAny**: `O(min(n, position))` → worst-case `O(n)` to reach deletion point or last node.
- **display**: `O(n)` to traverse all nodes once.
- **Space Complexity**: `O(1)` auxiliary; nodes occupy `O(n)` heap memory.

**Note:** operations can be improved to `O(1)` for head insertion/deletion if a `tail` pointer is maintained. Current code uses only a `head` pointer.

---

## Complete C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int data) {
        this->data = data;
        this->next = NULL;
    }

    ~Node() {}
};

void InsertAtHead(Node* &head, int data) {
    Node* newNode = new Node(data);

    if (head == NULL) {
        head = newNode;
        newNode->next = head; // points to itself
        return;
    }

    // find last node to update its next to new head
    Node* curr = head;
    while (curr->next != head) {
        curr = curr->next;
    }
    newNode->next = head;
    curr->next = newNode;
    head = newNode;
}

void InsertAtAny(Node* &head, int data, int position) {
    if (position <= 1 || head == NULL) { // insert at head if pos==1 or list empty
        InsertAtHead(head, data);
        return;
    }

    int cnt = 1;
    Node* curr = head;
    // move to node at position-1 or to the last node if shorter list
    while (cnt < position - 1 && curr->next != head) {
        curr = curr->next;
        cnt++;
    }

    // inserting after curr
    Node* newNode = new Node(data);
    newNode->next = curr->next;
    curr->next = newNode;
}

void deletionAtAny(Node* &head, int position) {
    if (head == NULL) return;

    // delete first node
    if (position == 1) {
        // single node case
        if (head->next == head) {
            delete head;
            head = NULL;
            return;
        }

        // find last node
        Node* last = head;
        while (last->next != head) {
            last = last->next;
        }
        Node* toDelete = head;
        head = head->next;
        last->next = head;
        toDelete->next = NULL;
        delete toDelete;
        return;
    }

    // delete at position > 1
    int cnt = 1;
    Node* curr = head;
    while (cnt < position - 1 && curr->next != head) {
        curr = curr->next;
        cnt++;
    }

    // if next is head, position was out of range (no node to delete)
    if (curr->next == head) return;

    Node* toDelete = curr->next;
    curr->next = toDelete->next;
    toDelete->next = NULL;
    delete toDelete;
}

void display(Node* head) {
    if (head == NULL) {
        cout << "List is empty\n";
        return;
    }

    Node* temp = head;
    do {
        cout << temp->data << "->";
        temp = temp->next;
    } while (temp != head);
    cout << "(head)\n";
}

int main() {
    Node* head = NULL;

    InsertAtAny(head, 10, 1);
    InsertAtAny(head, 20, 2);
    InsertAtAny(head, 40, 3);
    InsertAtAny(head, 50, 4);
    InsertAtAny(head, 60, 5);
    InsertAtAny(head, 30, 3);

    display(head); 

    deletionAtAny(head, 6); 
    display(head);

    deletionAtAny(head, 2); 
    display(head);

    return 0;
}
