# Doubly Linked List

A **doubly linked list** consists of nodes that each hold data plus `next` and `previous` pointers, allowing forward and backward movement through the structure.  
This bidirectional linkage simplifies end operations and deleting a known node, since both neighbors can be rewired directly without scanning from the head.

---

## Advantages

- **Bidirectional traversal**: moving both forward and backward is direct and useful for algorithms needing reverse iteration or backtracking.  
- **Efficient local updates**: given a node pointer, deletion is **O(1)** because both `prev` and `next` can be updated in-place without searching for the predecessor.  
- **End operations**: with a tail pointer, insertions and deletions at the end are **O(1)**, complementing **O(1)** operations at the head.  

---

## Time Complexity

| Operation                          | Time Complexity | Notes |
|------------------------------------|-----------------|-------|
| Insertion at head                  | **O(1)**        | Insert before current head |
| Insertion at tail (no tail ptr)    | **O(n)**        | Traverse to last node |
| Insertion at tail (with tail ptr)  | **O(1)**        | Update tail pointer |
| Insertion at any position by index | **O(n)**        | Traverse to position, then **O(1)** relink |
| Deletion at head                   | **O(1)**        | Move head and fix `prev` |
| Deletion at tail (no tail ptr)     | **O(n)**        | Traverse to last node |
| Deletion at tail (with tail ptr)   | **O(1)**        | Update tail to `tail->prev` |
| Deletion at any position by index  | **O(n)**        | Traverse to node, then **O(1)** unlink |
| Traversal (print/scan)             | **O(n)**        | Visit each node |

**Note:** If a direct pointer to the target node is already known, deletion or insertion adjacent to that node is **O(1)**.  
The **O(n)** cost comes from locating the node by position or value.

---

## C++ Implementation

```cpp
// Doubly Linked List (Insertion, Deletion and Printing via traversal)

#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node* prev;

    Node(int data) {
        this->data = data;
        this->next = NULL;
        this->prev = NULL;
    }

    ~Node() {
        int val = this -> data;
        if(next != NULL) {
            delete next;
            next = NULL;
        }
        cout << "memory free for node with data "<< val << endl;
    }
};

void insertAtHead(Node* &head, Node* &tail, int data) {
    Node* tempNode = new Node(data);

    // If list is empty
    if (head == NULL) {
        head = tempNode;
        tail = tempNode;
        return;
    }

    tempNode->next = head;
    head->prev = tempNode;
    head = tempNode;
}

void insertAtTail(Node* &head, Node* &tail, int data) {
    Node* tempNode = new Node(data);

    // If list is empty
    if (tail == NULL) {
        head = tempNode;
        tail = tempNode;
        return;
    }

    tail->next = tempNode;
    tempNode->prev = tail;
    tail = tempNode;
}

void insertAtAnyLocation(Node* &head, Node* &tail, int position, int data) {
    // insert at start
    if (position == 1) {
        insertAtHead(head, tail, data);
        return;
    }

    int count = 1;
    Node* temp = head;
    while (count < position - 1 && temp->next != NULL) {
        temp = temp->next;
        count++;
    }

    // inserting at last
    if (temp->next == NULL) {
        insertAtTail(head, tail, data);
        return;
    }

    // inserting in between
    Node* tempNode = new Node(data);
    tempNode->next = temp->next;
    temp->next->prev = tempNode;
    tempNode->prev = temp;
    temp->next = tempNode;
}

void Deletion(int position, Node* &head, Node* &tail) {
    // empty list
    if (head == NULL) {
        cout << "List is empty, nothing to delete." << endl;
        return;
    }

    // deleting first node
    if (position == 1) {
        Node* temp = head;
        head = head->next;

        // if list had only one node
        if (head == NULL) {
            tail = NULL;
        } else {
            head->prev = NULL;
        }

        temp->next = NULL;
        delete temp;
        return;
    }

    // deleting in middle or end
    Node* curr = head;
    int cnt = 1;
    while (cnt < position && curr != NULL) {
        curr = curr->next;
        cnt++;
    }

    // if position > length
    if (curr == NULL) {
        cout << "Position out of range!" << endl;
        return;
    }

    // if last node
    if (curr->next == NULL) {
        tail = curr->prev;
        tail->next = NULL;
        curr->prev = NULL;
        delete curr;
        return;
    }

    // deleting middle node
    Node* prevNode = curr->prev;
    Node* nextNode = curr->next;

    prevNode->next = nextNode;
    nextNode->prev = prevNode;

    curr->next = NULL;
    curr->prev = NULL;
    delete curr;
}

void printing(Node* head) {            // Linked List Traversing.
    Node* temp = head;
    while (temp != NULL) {
        cout << temp->data << "->";
        temp = temp->next;
    }
    cout << "NULL" << endl;
}

int main() {
    Node* head = NULL;  // start with empty list
    Node* tail = NULL;

    insertAtHead(head, tail, 10);   // head and tail created
    printing(head);                 // 10->NULL

    insertAtHead(head, tail, 20);   // insert at head
    printing(head);                 // 20->10->NULL

    insertAtTail(head, tail, 30);   // insert at tail
    printing(head);                 // 20->10->30->NULL

    insertAtAnyLocation(head, tail, 2, 40);  // insert at pos 2
    printing(head);                          // 20->40->10->30->NULL

    cout << "Head: " << head->data << endl;  // 20
    cout << "Tail: " << tail->data << endl;  // 30

    Deletion(2,head,tail);
    printing(head);

    return 0;
}
