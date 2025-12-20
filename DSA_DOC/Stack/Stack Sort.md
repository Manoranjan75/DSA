# Stack Sort (Using Recursion)

Given a stack of integers, sort the stack **using recursion only**.  
You are **not allowed to use any extra data structure** (like arrays, vectors, or another stack).  
Only the **call stack (recursion)** is permitted.

---

## Core Idea

The idea is similar to **recursive insertion sort**:

1. **Sort the stack recursively** by removing the top element.
2. **Insert the removed element back** into the sorted stack at its **correct position**.

This is achieved using two recursive functions:
- `Stack_sort()` → sorts the stack
- `InsertAtRightPlace()` → inserts an element into its correct sorted position

---

## Approach Explanation

### 1. `Stack_sort(stack<int>& st)`
- Base Case:  
  If the stack is empty, it is already sorted.
- Recursive Step:
  - Pop the top element.
  - Recursively sort the remaining stack.
  - Insert the popped element back into the sorted stack using `InsertAtRightPlace`.

### 2. `InsertAtRightPlace(stack<int>& st, int element)`
- Base Case:
  - If stack is empty **OR**
  - `element` is smaller than the top element  
  → push the element directly.
- Recursive Step:
  - Pop the top element.
  - Recursively find the correct position.
  - Push the popped element back.

This ensures elements are placed in **ascending order** (smallest at bottom, largest at top).

---

## Dry Run (Conceptual)

Initial stack (top → bottom):
11 2 32 3 41


After sorting:
2 3 11 32 41 


(When displayed by popping, it prints in descending order because the largest element is on top.)

---

## Time & Space Complexity

- **Time Complexity:** `O(n²)`  
  Each insertion may traverse the entire stack.

- **Space Complexity:** `O(n)`  
  Due to recursion call stack.

---

## Complete C++ Code 

```cpp
#include<bits/stdc++.h>
using namespace std;

void InsertAtRightPlace(stack<int> &st, int element){
    // Base case
    if(st.empty() || element < st.top()){
        st.push(element);
        return;
    }

    int top = st.top();
    st.pop();

    InsertAtRightPlace(st, element);
    st.push(top);
}

void Stack_sort(stack<int> &st){
    // Base case
    if(st.empty()){
        return;
    }

    int top = st.top();
    st.pop();

    Stack_sort(st);
    InsertAtRightPlace(st, top);
}

void display(stack<int> st){
    while(!st.empty()){
        cout << st.top() << " ";
        st.pop();
    }
    cout << endl;
}

int main(){
    stack<int> st;
    st.push(41);
    st.push(3);
    st.push(32);
    st.push(2);
    st.push(11);

    display(st);   // Before sorting

    Stack_sort(st);

    display(st);   // After sorting

    return 0;
}

