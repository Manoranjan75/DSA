# Check if a Linked List is a Palindrome (C++)

## Problem Statement

Given the head of a singly linked list, determine whether the list is a palindrome.

A linked list is a palindrome if the sequence of its node values reads the same forward and backward.

### Examples

1.  
List: `1 → 2 → 3 → 2 → 1`  
Output: `true` (palindrome)

2.  
List: `1 → 2 → 3`  
Output: `false` (not a palindrome)

---

## Approach (Fast–Slow Pointer + Reverse Second Half)

We can solve this in O(n) time and O(1) extra space using these steps:

1. **Find the middle of the list** using fast and slow pointers:
   - `slow` moves one step at a time.
   - `fast` moves two steps at a time.
   - When `fast` reaches the end, `slow` will be at the middle.

2. **Reverse the second half** of the list starting from `slow`.

3. **Compare the first half and the reversed second half** node by node:
   - Move one pointer from the head.
   - Move the other pointer from the head of the reversed second half.
   - If all corresponding values are equal, it is a palindrome.

4. (Optional) Restore the list by reversing the second half again.

---

## C++ Implementation

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

// Utility function to append a node at the end
void append(Node*& head, int val) {
    Node* newNode = new Node(val);
    if (head == NULL) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next != NULL)
        temp = temp->next;
    temp->next = newNode;
}

// Utility function to print the list
void printList(Node* head) {
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

// Reverse a linked list starting from 'head'
Node* reverseList(Node* head) {
    Node* prev = NULL;
    Node* curr = head;

    while (curr != NULL) {
        Node* nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev; // new head of reversed list
}

// Check if linked list is palindrome
bool isPalindrome(Node* head) {
    if (head == NULL || head->next == NULL)
        return true;

    // Step 1: Find middle (slow will point to middle)
    Node* slow = head;
    Node* fast = head;

    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Step 2: Reverse second half starting from slow
    Node* secondHalfHead = reverseList(slow);

    // Step 3: Compare first half and reversed second half
    Node* p1 = head;
    Node* p2 = secondHalfHead;
    bool palindrome = true;

    while (p2 != NULL) { // only need to traverse second half
        if (p1->data != p2->data) {
            palindrome = false;
            break;
        }
        p1 = p1->next;
        p2 = p2->next;
    }

    // Optional Step 4: Restore original list (reverse again)
    reverseList(secondHalfHead);

    return palindrome;
}

int main() {
    // Example 1: Palindrome list
    Node* head1 = NULL;
    append(head1, 1);
    append(head1, 2);
    append(head1, 3);
    append(head1, 2);
    append(head1, 1);

    cout << "List 1: ";
    printList(head1);
    cout << "Is palindrome? " << (isPalindrome(head1) ? "Yes" : "No") << endl;

    // Example 2: Non-palindrome list
    Node* head2 = NULL;
    append(head2, 1);
    append(head2, 2);
    append(head2, 3);

    cout << "List 2: ";
    printList(head2);
    cout << "Is palindrome? " << (isPalindrome(head2) ? "Yes" : "No") << endl;

    return 0;
}
