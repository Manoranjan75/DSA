# Reverse a Stack Using Recursion 

Given a stack of integers, reverse the stack **using recursion only**.  
You are **not allowed** to use any extra data structure (like array, vector, or another stack).  
Only recursion (call stack) is permitted.

---

## Core Idea

To reverse a stack recursively, we use **two recursive functions**:

1. **`reverseStack()`**  
   - Removes elements one by one from the top.
   - Recursively reverses the remaining stack.
   - Inserts the removed element at the **bottom** of the stack.

2. **`InsertAtBottom()`**  
   - Inserts a given element at the bottom of the stack using recursion.

This approach mimics how reversal works by temporarily emptying the stack and rebuilding it in reverse order.

---

## Approach Explanation

### 1. `reverseStack(stack<int>& st)`
- **Base case:**  
  If the stack is empty, return.
- **Recursive step:**  
  - Pop the top element.
  - Recursively reverse the remaining stack.
  - Insert the popped element at the bottom using `InsertAtBottom()`.

### 2. `InsertAtBottom(stack<int>& st, int element)`
- **Base case:**  
  If the stack is empty, push the element (this places it at the bottom).
- **Recursive step:**  
  - Pop the top element.
  - Recursively call `InsertAtBottom()`.
  - Push the popped element back.

---

## Dry Run (Conceptual)

Initial stack (top → bottom):
1 2 3 4 5

After reversing:
5 4 3 2 1


---

## Time & Space Complexity

- **Time Complexity:** `O(n²)`  
  Each element insertion at bottom may traverse the entire stack.
- **Space Complexity:** `O(n)`  
  Due to recursion call stack.

---

## Complete C++ Code 

```cpp
#include<bits/stdc++.h>
using namespace std;

void InsertAtBottom (stack<int> &st, int element){
    // Base case
    if(st.empty()){
        st.push(element);
        return;
    }

    int top = st.top();
    st.pop();

    InsertAtBottom(st, element);
    st.push(top);
}

void reverseStack (stack<int> &st){
    // Base case
    if(st.empty()){
        return;
    }

    int top = st.top();
    st.pop();

    reverseStack(st);
    InsertAtBottom(st, top);
}

void display(stack<int> st){
    while(!st.empty()){
        cout << st.top();
        st.pop();
    }
    cout << endl;
}

int main(){
    stack<int> st;
    for(int i = 5; i > 0; i--){
        st.push(i);
    }

    display(st);       // Before reversing
    reverseStack(st);
    display(st);       // After reversing

    return 0;
}
