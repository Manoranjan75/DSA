# Redundant Brackets
Given a **valid mathematical expression** in the form of a string, determine whether the expression contains **redundant (unnecessary) brackets**.

### Definition  
A pair of brackets is said to be **redundant** if removing them does **not change the meaning** of the expression.

The expression contains only:
- `'(' , ')'`
- Operators: `'+' , '-' , '*' , '/'`
- Lowercase English letters

---

## Examples

| Expression        | Result | Reason |
|-------------------|--------|--------|
| `(a+b)`           | false  | Brackets are required |
| `((a+b))`         | true   | Extra outer brackets |
| `(a+(b))`         | true   | `(b)` is redundant |
| `(a+(b*c))`       | false  | Inner brackets needed |
| `(a+(b*(c)))`     | true   | `(c)` is redundant |

---

## Approach (Using Stack)

### Key Idea  
Whenever we encounter a closing bracket `')'`, we check **what is inside the matching '('**.

- If **no operator** exists between `'('` and `')'`, then the brackets are **redundant**.
- If **at least one operator** exists, then the brackets are **useful**.

---

### Algorithm Steps

1. Create a stack of characters.
2. Traverse the string character by character:
   - If the character is `'('` or an operator (`+ - * /`), push it onto the stack.
3. If the character is `')'`:
   - Assume brackets are redundant (`ans = true`).
   - Pop elements from the stack until `'('` is found:
     - If any operator is found, set `ans = false`.
   - If `ans` remains `true`, redundant brackets exist → return `true`.
   - Pop `'('` from the stack.
4. If the loop finishes, return `false`.

---

## Why This Works

- Redundant brackets **do not enclose any operator**.
- Stack allows us to inspect the contents inside each bracket pair efficiently.
- Each character is pushed and popped once → optimal solution.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(n)` (stack usage)

---

## Complete C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

bool redundantBrcakets(string str){
    stack<char> st;

    for(int i = 0; i < str.length(); i++){
        char ch = str[i];

        if(ch == '(' || ch == '+' || ch == '-' || ch == '*' || ch == '/'){
            st.push(ch);
        }
        else{
            // ch == ')' or lowercase alphabet
            if(ch == ')'){
                bool ans = true;

                while(!st.empty() && st.top() != '('){
                    char topElemenet = st.top();
                    st.pop();

                    if(topElemenet == '+' || topElemenet == '-' ||
                       topElemenet == '*' || topElemenet == '/'){
                        ans = false;
                    }
                }

                if(ans == true){
                    return true; // redundant brackets found
                }

                st.pop(); // pop '('
            }
        }
    }
    return false;
}

int main(){
    string str = "(a+(b*(c))";
    cout << redundantBrcakets(str);
    return 0;
}
