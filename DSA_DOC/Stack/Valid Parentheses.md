#  Valid Parentheses (C++)

---

##  Problem (Brief)

Given a string containing only the characters `(`, `)`, `{`, `}`, `[` and `]`,  
determine whether the string is **valid**.

A string is valid if:

- Every opening bracket has a corresponding closing bracket of the same type.  
- Brackets close in the correct **LIFO (Last In, First Out)** order.

---

##  Idea

We use a **stack** to ensure proper nesting and matching of brackets.

###  Algorithm Steps

1. Traverse the string character by character.
2. If it’s an **opening bracket** (`(`, `{`, `[`), **push** it onto the stack.
3. If it’s a **closing bracket**:
   - The stack must **not be empty**.
   - The **top** of the stack must be the matching opening bracket.
   - If not, the string is invalid.
4. After traversing, the stack must be **empty** (no unmatched openings).

---

##  C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isValid(const string &s) {
    unordered_map<char, char> match = {
        {')', '('}, {']', '['}, {'}', '{'}
    };
    stack<char> st;

    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            st.push(c);  // opening bracket
        } else {
            // closing bracket -> must match stack top
            if (st.empty() || st.top() != match[c])
                return false;
            st.pop();
        }
    }
    return st.empty();  // valid if all brackets matched
}

int main() {
    vector<string> tests = {"({[]})", "([)]", "()", "({[})", ""};
    for (auto &t : tests) {
        cout << "\"" << t << "\" -> " << (isValid(t) ? "valid" : "invalid") << '\n';
    }
    return 0;
}
