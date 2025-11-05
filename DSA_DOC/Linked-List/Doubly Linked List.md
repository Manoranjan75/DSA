
###  Key Features
- Traversal can start from any node.
- Useful in round-robin scheduling, buffering, and implementing queues.

---

##  Operations Covered
1. **Insert at End**
2. **Insert at Beginning**
3. **Delete a Node**
4. **Display the List**

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

// Node structure
class Node {
public:
    int data;
    Node* next;

    Node(int val) {
        data = val;
        next = nullptr;
    }
};

// Insert at end
void insertAtEnd(Node*& head, int val) {
    Node* newNode = new Node(val);

    // Case 1: Empty list
    if (head == nullptr) {
        head = newNode;
        head->next = head; // circular link
        return;
    }

    // Case 2: Non-empty list
    Node* temp = head;
    while (temp->next != head)
        temp = temp->next;

    temp->next = newNode;
    newNode->next = head;
}

// Insert at beginning
void insertAtBeginning(Node*& head, int val) {
    Node* newNode = new Node(val);

    if (head == nullptr) {
        head = newNode;
        head->next = head;
        return;
    }

    Node* temp = head;
    while (temp->next != head)
        temp = temp->next;

    temp->next = newNode;
    newNode->next = head;
    head = newNode;
}

// Delete a node by value
void deleteNode(Node*& head, int key) {
    if (head == nullptr) {
        cout << "List is empty!" << endl;
        return;
    }

    Node* curr = head;
    Node* prev = nullptr;

    // If the head itself holds the key
    if (curr->data == key) {
        Node* temp = head;

        // Find the last node
        while (temp->next != head)
            temp = temp->next;

        // If there is only one node
        if (temp == head) {
            delete head;
            head = nullptr;
            return;
        }

        temp->next = head->next;
        Node* delNode = head;
        head = head->next;
        delete delNode;
        return;
    }

    // Search for the key
    do {
        prev = curr;
        curr = curr->next;

        if (curr->data == key) {
            prev->next = curr->next;
            delete curr;
            return;
        }
    } while (curr != head);

    cout << "Node with value " << key << " not found!" << endl;
}

// Display the circular linked list
void display(Node* head) {
    if (head == nullptr) {
        cout << "List is empty!" << endl;
        return;
    }

    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);

    cout << endl;
}

int main() {
    Node* head = nullptr;

    insertAtEnd(head, 10);
    insertAtEnd(head, 20);
    insertAtEnd(head, 30);
    insertAtBeginning(head, 5);

    cout << "Circular Linked List: ";
    display(head);

    deleteNode(head, 20);
    cout << "After deleting 20: ";
    display(head);

    deleteNode(head, 5);
    cout << "After deleting 5 (head): ";
    display(head);

    return 0;
}
