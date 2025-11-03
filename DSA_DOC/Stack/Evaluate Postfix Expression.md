#  Evaluate Postfix Expression (Using Stack) — C++

---

##  Problem Statement

You are given a **postfix expression** (also known as **Reverse Polish Notation**, or **RPN**).  
Your task is to **evaluate** the expression and return the final result.

In a **postfix expression**, the **operator comes after its operands**.

---
| Operation | Complexity | Explanation                    |
| --------- | ---------- | ------------------------------ |
| **Time**  | O(n)       | Single traversal of expression |
| **Space** | O(n)       | Stack used for operands        |

---
###  Example

| Infix Expression | Postfix Expression | Result |
|------------------|--------------------|---------|
| (2 + 3) * 4 | 2 3 + 4 * | 20 |

---

##  Example 1

### Input:

- expression = "231*+9-"

### Output:
- -4
### Explanation:
- 2 3 1 * + 9 -
- = (2 + (3 × 1)) - 9
- = 5 - 9
- = -4

```cp
#include <bits/stdc++.h>
using namespace std;

int evaluatePostfix(string exp) {
    stack<int> st;

    for (char c : exp) {
        if (isdigit(c)) {
            st.push(c - '0');  // convert char to int
        } 
        else {
            int b = st.top(); st.pop();
            int a = st.top(); st.pop();

            switch (c) {
                case '+': st.push(a + b); break;
                case '-': st.push(a - b); break;
                case '*': st.push(a * b); break;
                case '/': st.push(a / b); break;
            }
        }
    }
    return st.top();
}

int main() {
    string exp;
    cout << "Enter postfix expression: ";
    cin >> exp;

    cout << "Result = " << evaluatePostfix(exp) << endl;
    return 0;
}


