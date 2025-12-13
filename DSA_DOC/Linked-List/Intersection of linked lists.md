# Intersection of Two Linked Lists 

Given the heads of two singly linked lists `headA` and `headB`, determine the node at which the two lists **intersect**.  
The intersection is based on **reference (memory address)**, not on node value.  
If the two linked lists do **not** intersect, return `NULL`.

---

## Approach (Two-Pointer Technique)

1. Use two pointers:
   - `pA` starting at `headA`
   - `pB` starting at `headB`
2. Traverse both lists simultaneously.
3. When `pA` reaches the end of List A, redirect it to `headB`.
4. When `pB` reaches the end of List B, redirect it to `headA`.
5. Eventually:
   - If an intersection exists, both pointers meet at the intersection node.
   - If no intersection exists, both pointers become `NULL` at the same time.

### Why this works
- Each pointer traverses exactly `lengthA + lengthB` nodes.
- The length difference between lists is automatically balanced.
- No extra memory is required.

---

## Time & Space Complexity

- **Time Complexity:** `O(n + m)`  
  where `n` is the length of List A and `m` is the length of List B.
- **Space Complexity:** `O(1)`  
  constant extra space.

---

## C++ Code

```cpp
/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
    if (headA == NULL || headB == NULL)
        return NULL;

    ListNode* pA = headA;
    ListNode* pB = headB;

    while (pA != pB) {
        pA = (pA == NULL) ? headB : pA->next;
        pB = (pB == NULL) ? headA : pB->next;
    }

    // Either intersection node or NULL
    return pA;
}
