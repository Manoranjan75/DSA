# Rotate Linked List — Complete File

Given the head of a singly linked list and an integer `k`, rotate the list to the **right** by `k` places.

Example:

- Input: 1 → 2 → 3 → 4 → 5, k = 2
- Output: 4 → 5 → 1 → 2 → 3


To rotate:
- Take last `k` nodes and bring them to the front.

---

##  Approach

### Steps

1. **Edge cases**
   - If list is empty, only one node, or `k = 0`, return as is.

2. **Find length and last node**
   - Traverse the list to count nodes (`cnt`) and reach the last node (`curr`).

3. **Connect last node to head**
   - Temporarily make the list circular:  
     `curr->next = head`.

4. **Compute effective rotation**
   - `rotate = k % cnt`  
     Because rotating by list length gives the same list.

5. **Find new tail and new head**
   - New tail is at position `(cnt - rotate)` from the start.
   - New head is `newTail->next`.

6. **Break the circular link**
   - `newTail->next = NULL`.

7. Return `newHead`.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)` — single pass to count nodes and another partial pass to find new tail.
- **Space Complexity:** `O(1)` — no extra data structures used.

---

## C++ Code

```cpp
ListNode* rotateRight(ListNode* head, int k) {
    if (!head || !head->next || k == 0) 
        return head;

    int cnt = 1;
    ListNode* curr = head;

    // Count length and go to last node
    while (curr->next != NULL) {
        cnt++;
        curr = curr->next;
    }

    // Effective rotation
    int rotate = k % cnt;

    // Make it circular
    curr->next = head;

    // Find new tail = (cnt - rotate)-th node
    int stepsToNewTail = cnt - rotate;
    ListNode* newTail = head;

    for (int i = 1; i < stepsToNewTail; ++i) {
        newTail = newTail->next;
    }

    // New head
    ListNode* newHead = newTail->next;

    // Break the ring
    newTail->next = nullptr;

    return newHead;
}
