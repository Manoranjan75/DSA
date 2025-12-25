# Insert Element at Bottom of a Stack (Using Recursion)

Given a stack of integers, insert a given element **at the bottom of the stack** using **recursion only**.  
You are **not allowed** to use any extra data structure (like arrays, vectors, or another stack).

---

## Core Idea

To insert an element at the **bottom** of a stack using recursion:

1. **Pop elements one by one** until the stack becomes empty.
2. **Insert the element** when the stack is empty (this places it at the bottom).
3. **Push back all popped elements** in the same order as before.

This uses the **call stack** to temporarily hold elements.

---

## Approach Explanation

### Function: `InsertAtBottom(stack<int>& st, int element)`

- **Base Case**  
  If the stack is empty, push the element and return.

- **Recursive Step**  
  - Pop the top element.
  - Recursively call `InsertAtBottom()` to reach the bottom.
  - Push the popped element back.

This guarantees that the new element is placed at the bottom and the original order is preserved above it.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`  
  Each element is popped and pushed once.

- **Space Complexity:** `O(n)`  
  Due to recursion call stack.

---

## Complete C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

void InsertAtBottom(stack<int> &st, int element){
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
    st.push(6);

    display(st);   // Before insertion at bottom

    InsertAtBottom(st, 7);

    display(st);   // After insertion at bottom

    return 0;
}
