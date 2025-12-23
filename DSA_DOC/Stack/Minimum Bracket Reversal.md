# Minimum Bracket Reversal

You are given a string consisting only of **'{'** and **'}'**.  
Your task is to determine the **minimum number of bracket reversals** needed to make the expression **balanced**.  
If it is **not possible** to balance the string, return **-1**.

---

## Key Observation  
- A balanced braces expression must have **even length**.  
  If length is **odd**, return `-1`.

After removing all valid pairs `{}`, the leftover characters will be some number of `{` and `}`.  
Let:
- `a` = count of leftover `{`
- `b` = count of leftover `}`

The minimum reversals required is:
(a + 1) / 2 + (b + 1) / 2


This works because:
- `{{` needs 1 reversal
- `}}` needs 1 reversal
- `}{` type patterns need 2 reversals

---

## Approach (Stack Method)

1. Return `-1` if string length is odd.
2. Use a stack:
   - Push `{`
   - When encountering `}`, pop if top is `{` (valid pair), else push.
3. After processing, the stack contains only **unbalanced brackets**.
4. Count leftover `{` as `a` and leftover `}` as `b`.
5. Apply formula to get final answer.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)` due to stack

---

## Complete C++ Code

```cpp
#include<bits/stdc++.h>
using namespace std;

int MinimumBracketsReversal(const string &str) {

    // Condition: Odd length can never be balanced
    if (str.length() % 2 != 0) {
        return -1;
    }

    stack<char> st;

    // Remove valid pairs using stack
    for(char ch : str) {
        if(ch == '{') {
            st.push(ch);
        } else {
            if(!st.empty() && st.top() == '{') {
                st.pop();   // Valid pair removed
            } else {
                st.push(ch);
            }
        }
    }

    // Count leftover braces
    int a = 0, b = 0;

    while(!st.empty()) {
        if(st.top() == '{')
            a++;
        else
            b++;
        st.pop();
    }

    // Apply formula
    return ((a + 1) / 2) + ((b + 1) / 2);
}

int main() {
    string str = "{{}}{{";
    cout << MinimumBracketsReversal(str);
    return 0;
}

