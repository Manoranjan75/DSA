#  Reverse a Queue (C++)

---

##  Problem Statement

Given a queue, reverse its elements **so that the front becomes the rear and vice versa**.

You can use either:
- **Recursion**, or  
- **An auxiliary stack**

Your task: Modify the queue **in place** and maintain the order after reversal.

---

##  Example

### Input:
Queue: 10 20 30 40 50


### Output:
Reversed Queue: 50 40 30 20 10



---

## ⚙️ Approach 1 — Using Stack (Iterative)

1. Create an empty **stack**.
2. Dequeue elements from the queue and push them onto the stack.
3. Pop all elements from the stack and enqueue them back into the queue.
4. Result: Queue is reversed.

### Why this works:
- The **stack reverses** order because it’s LIFO (Last In, First Out).
- Then, re-enqueuing puts them back in the reversed sequence.

---

##  C++ Code (Using Stack)

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to reverse a queue using stack
void reverseQueue(queue<int> &q) {
    stack<int> s;

    // Step 1: Push all elements from queue to stack
    while (!q.empty()) {
        s.push(q.front());
        q.pop();
    }

    // Step 2: Pop all elements from stack back to queue
    while (!s.empty()) {
        q.push(s.top());
        s.pop();
    }
}

int main() {
    queue<int> q;
    q.push(10);
    q.push(20);
    q.push(30);
    q.push(40);
    q.push(50);

    cout << "Original Queue: ";
    queue<int> temp = q;
    while (!temp.empty()) {
        cout << temp.front() << " ";
        temp.pop();
    }
    cout << endl;

    reverseQueue(q);

    cout << "Reversed Queue: ";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;

    return 0;
}
