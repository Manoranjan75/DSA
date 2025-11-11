# Detect and Remove Cycle in a Singly Linked List (C++)

## Problem
Given the head of a singly linked list, detect whether the list contains a cycle (loop).  
If a cycle exists, remove the cycle so that the list becomes linear (the last node's `next` becomes `nullptr`).  
Return a boolean indicating whether a cycle was found and removed.

---

## Idea / Approach
Use **Floyd’s Cycle-Finding** algorithm:

1. **Detect cycle**:
   - Use two pointers: `slow` moves one step, `fast` moves two steps.
   - If `slow` and `fast` meet, a cycle exists.
   - If `fast` or `fast->next` becomes `nullptr`, there is no cycle.

2. **Find start of the cycle**:
   - After detection (meeting point `meet`), set `ptr1 = head`.
   - Set `ptr2 = meet`.
   - If `ptr1 == ptr2`, the cycle starts at the head. To remove the cycle, advance `ptr2` until `ptr2->next == ptr1` (the last node in the loop) and set `ptr2->next = nullptr`.
   - Otherwise, move `ptr1` and `ptr2` one step at a time until `ptr1->next == ptr2->next`. Now `ptr2->next` is the cycle start. Set `ptr2->next = nullptr` to break the loop.

This removal method keeps the list nodes intact and uses constant extra space.

---

## Complexity
- Time: `O(n)` — detection and removal together traverse the list a constant number of times.
- Space: `O(1)` — only a few pointers used.

---

## C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Utility: append node at end (for building test lists)
void append(Node*& head, int val) {
    Node* newNode = new Node(val);
    if (!head) {
        head = newNode;
        return;
    }
    Node* t = head;
    while (t->next) t = t->next;
    t->next = newNode;
}

// Utility: create cycle for testing. Connect last node to node at position pos (0-based).
// If pos == -1, no cycle.
void createCycle(Node* head, int pos) {
    if (!head || pos < 0) return;
    Node* tail = head;
    Node* target = nullptr;
    int idx = 0;
    while (tail->next) {
        if (idx == pos) target = tail;
        tail = tail->next;
        idx++;
    }
    if (idx == pos) target = tail; // if pos points to last node
    if (target) tail->next = target;
}

// Detect cycle using Floyd's algorithm. If found, return meeting node; else return nullptr.
Node* detectCycle(Node* head) {
    Node* slow = head;
    Node* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return slow;
    }
    return nullptr;
}

// Remove cycle given head. Returns true if cycle was found and removed, false otherwise.
bool detectAndRemoveCycle(Node* head) {
    Node* meet = detectCycle(head);
    if (!meet) return false; // no cycle

    Node* ptr1 = head;
    Node* ptr2 = meet;

    // If the cycle starts at head
    if (ptr1 == ptr2) {
        // find the node pointing back to head
        while (ptr2->next != ptr1) ptr2 = ptr2->next;
        ptr2->next = nullptr;
        return true;
    }

    // Move both pointers until they meet at the node just before cycle start
    while (ptr1->next != ptr2->next) {
        ptr1 = ptr1->next;
        ptr2 = ptr2->next;
    }

    // ptr2->next is the start of the loop; break it
    ptr2->next = nullptr;
    return true;
}

// Print list (safe variant that stops after maxNodes to avoid infinite loop during debugging)
void printList(Node* head, int maxNodes = 100) {
    Node* t = head;
    int count = 0;
    while (t && count++ < maxNodes) {
        cout << t->data << " ";
        t = t->next;
    }
    if (t) cout << "... (possible cycle or truncated)";
    cout << endl;
}

int main() {
    // Example 1: list without cycle
    Node* head1 = nullptr;
    append(head1, 1);
    append(head1, 2);
    append(head1, 3);
    append(head1, 4);

    cout << "Before (no cycle): ";
    printList(head1);

    bool removed1 = detectAndRemoveCycle(head1);
    cout << "Cycle removed? " << (removed1 ? "Yes" : "No") << endl;
    cout << "After: ";
    printList(head1);

    cout << "---------------------------\n";

    // Example 2: list with cycle (last node points to node at index 1)
    Node* head2 = nullptr;
    for (int i = 1; i <= 7; ++i) append(head2, i);
    createCycle(head2, 1); // cycle starts at node with value 2

    // Dangerous to print directly; show detection and then a safe print after removal
    cout << "Cycle present? ";
    cout << (detectCycle(head2) ? "Yes" : "No") << endl;

    bool removed2 = detectAndRemoveCycle(head2);
    cout << "Cycle removed? " << (removed2 ? "Yes" : "No") << endl;

    cout << "After removal (linear list): ";
    printList(head2);

    // Cleanup omitted for brevity
    return 0;
}
