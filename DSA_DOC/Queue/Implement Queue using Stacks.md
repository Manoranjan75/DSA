#  Implement a Queue using Stacks (C++)

---

## Problem Statement

Design a **Queue (FIFO – First In First Out)** using **two Stacks (LIFO – Last In First Out)**.  
Your queue should support the following operations:

- **push(x)** — Insert an element into the queue.  
- **pop()** — Remove the element from the front of the queue.  
- **peek()** — Get the front element.  
- **empty()** — Check whether the queue is empty.  

You must use only **standard stack operations**:  
`push()`, `pop()`, `top()`, `empty()`, and `size()`.

---

| Operation   | Time Complexity | Explanation                             |
| ----------- | --------------- | --------------------------------------- |
| **push()**  | O(1)            | Pushes directly into `inStack`          |
| **pop()**   | Amortized O(1)  | Transfers only when `outStack` is empty |
| **peek()**  | Amortized O(1)  | Same as pop (lazy transfer)             |
| **empty()** | O(1)            | Constant-time check                     |

---

##  Example

### Input:

MyQueue q;
q.push(1);
q.push(2);
cout << q.peek();   // Output: 1
cout << q.pop();    // Output: 1
cout << q.empty();  // Output: 0

### Output:
- 1
- 1
- 0

### Code:

```cpp
#include <bits/stdc++.h>
using namespace std;

class MyQueue {
    stack<int> inStack, outStack;

public:
    // Push element x to the back of queue.
    void push(int x) {
        inStack.push(x);
    }

    // Removes the element from in front of queue.
    int pop() {
        peek(); // ensure outStack has the current front
        int val = outStack.top();
        outStack.pop();
        return val;
    }

    // Get the front element.
    int peek() {
        if (outStack.empty()) {
            while (!inStack.empty()) {
                outStack.push(inStack.top());
                inStack.pop();
            }
        }
        return outStack.top();
    }

    // Return whether the queue is empty.
    bool empty() {
        return inStack.empty() && outStack.empty();
    }
};

int main() {
    MyQueue q;
    q.push(1);
    q.push(2);

    cout << "Front element: " << q.peek() << endl; // 1
    cout << "Removed: " << q.pop() << endl;        // 1
    cout << "Is empty? " << q.empty() << endl;     // 0

    return 0;
}


