# Stack Implementation Using Array

A stack implemented using an array maintains elements in a fixed-size contiguous memory block with an index pointer tracking the top element.  
The **LIFO (Last In, First Out)** principle is enforced by only allowing additions and removals at the top position, making operations straightforward but limiting access to other elements.

---

## Advantages
- **Memory efficiency:** No extra memory overhead for pointers, unlike linked list implementations, resulting in compact storage.  
- **Fast access:** Constant-time **O(1)** operations for push, pop, peek, and isEmpty due to direct array indexing.  
- **Cache performance:** Contiguous memory layout improves cache locality, leading to better performance in practice.  
- **Simple implementation:** Straightforward logic without complex pointer management, reducing implementation errors.  
- **Predictable memory usage:** Fixed size allows precise memory allocation planning.  

---

## Disadvantages
- **Fixed size limitation:** Cannot grow beyond the initial capacity, leading to stack overflow if more elements are pushed.  
- **Memory waste:** May allocate more memory than needed if the actual usage is significantly less than capacity.  
- **No dynamic resizing:** Unlike linked lists, cannot adapt to varying workload sizes at runtime.  
- **Limited access:** Only the top element can be accessed, preventing random access to middle elements.  

---

## Time Complexity
All fundamental stack operations achieve optimal constant-time performance due to direct array access.

| Operation  | Time Complexity | Description |
|------------|-----------------|-------------|
| Push       | **O(1)**        | Direct insertion at top index |
| Pop        | **O(1)**        | Decrement top index |
| Peek/Top   | **O(1)**        | Access element at top index |
| isEmpty    | **O(1)**        | Check if top equals -1 |
| isFull     | **O(1)**        | Check if top equals size-1 |

> **Note:** Space complexity is **O(n)** where *n* is the maximum capacity, regardless of actual elements stored.

---

## Code

Below is a **C++ implementation** of an array-based stack with push, pop, peek, and isEmpty operations, including overflow/underflow error handling.  
The implementation uses a `top` index starting at `-1` to indicate an empty stack, incrementing for each push and decrementing for each pop.

```cpp
// Stack implementation using Array.

#include <bits/stdc++.h>
using namespace std;

class Stack {
public:
    int* arr;
    int size;
    int top;

    Stack(int size) {
        this->size = size;
        arr = new int[size];
        top = -1;
    }

    void push(int data) {
        if (top == size - 1) {
            cout << "Stack Overflow" << endl;
        } else {
            top++;
            arr[top] = data;
        }
    }

    void pop() {
        if (top < 0) {
            cout << "Stack is already empty" << endl;
        } else {
            top--;
        }
    }

    void peak() {
        if (top == -1) {
            cout << "Stack is empty, no top element." << endl;
        } else {
            cout << "Top element of stack: " << arr[top] << endl;
        }
    }

    void isEmpty() {
        if (top == -1) {
            cout << "Stack is empty" << endl;
        } else {
            cout << "Stack is not empty" << endl;
        }
    }

    ~Stack() {
        delete[] arr;
    }
};

int main() {
    Stack st(5);
    st.isEmpty();
    st.push(10);
    st.push(20);
    st.push(30);
    st.push(40);
    st.push(50);
    st.push(60); // This should show Overflow

    st.peak();
    st.pop();
    st.pop();

    st.peak();
    st.isEmpty();

    return 0;
}
