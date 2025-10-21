#  Check for Valid Parentheses (C++)

---

##  Problem Statement

Given a string containing only `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`,  
determine if it is **valid**.

A string is valid if:

1. Every opening bracket has a **corresponding closing bracket** of the same type.  
2. Brackets **close in the correct order**.

---

###  Examples

- "({[]})" → ✅ valid
- "([)]" → ❌ invalid
- "()" → ✅ valid

2. Traverse the string:
- If it’s an **opening bracket**, push it onto the stack.
- If it’s a **closing bracket**:
  - Stack must not be empty.
  - The top of the stack must match the corresponding opening bracket.
  - If not → return `false`.
  - Otherwise, pop the top element.
3. After traversal:
- If the stack is empty → return `true`.
- Otherwise → return `false`.

---

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isValid(const string &s) {
 unordered_map<char, char> match = {
     {')', '('},
     {']', '['},
     {'}', '{'}
 };
 stack<char> st;

 for (char c : s) {
     if (c == '(' || c == '[' || c == '{') {
         st.push(c);
     } else {
         if (st.empty() || st.top() != match[c])
             return false;
         st.pop();
     }
 }
 return st.empty();
}

int main() {
 vector<string> tests = {"({[]})", "([)]", "()", "({[})"};
 for (auto &t : tests) {
     cout << t << " -> " << (isValid(t) ? "valid" : "invalid") << '\n';
 }
 return 0;
}
