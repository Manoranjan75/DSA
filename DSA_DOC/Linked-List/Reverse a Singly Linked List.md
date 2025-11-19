# Reverse a Linked List (Iterative + Recursive)

## Problem Statement
Given the head of a singly linked list, reverse the list and return the new head.

### Example
Input:  
1 → 2 → 3 → 4 → 5 → NULL  

Output:  
5 → 4 → 3 → 2 → 1 → NULL

---

# Approach 1: Iterative Method

We use three pointers:

- prev  
- curr  
- nextNode  

We move through the list and reverse links one by one.

## C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(NULL) {}
};

// Iterative way

Node* reverseList(Node* head) {
    Node* prev = NULL;
    Node* curr = head;

    while (curr != NULL) {
        Node* nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev;
}

void printList(Node* head) {
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}


// Recursive way

Node* reverseRecursive(Node* head) {
    if (head == NULL || head->next == NULL)
        return head;

    Node* newHead = reverseRecursive(head->next);

    head->next->next = head;
    head->next = NULL;

    return newHead;
}


int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);

    cout << "Original List: ";
    printList(head);

    head = reverseList(head);

    cout << "Reversed List: ";
    printList(head);

    return 0;
}
