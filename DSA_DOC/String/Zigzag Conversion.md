#  Zigzag Conversion (C++)

---

##  Problem Statement

You are given a string `s` and an integer `numRows`.  
Rearrange the characters of the string in a **zigzag pattern** (as if written diagonally down and up),  
then read the result **row by row**.

---

##  Example

**Input:**

- s = "PAYPALISHIRING", numRows = 3

**Zigzag pattern:**

- P A H N
- A P L S I I G
- Y I R

**Reading row-wise:**
- "PAHNAPLSIIGYIR"

**Output:**
- PAHNAPLSIIGYIR


---

## ⚙️ Approach

We simulate the zigzag pattern by maintaining a list of strings (one for each row).

### Steps:
1. Create a `vector<string>` with one string for each row.
2. Traverse each character of the input string:
   - Add it to the current row.
   - Change direction (down or up) when reaching the **first** or **last** row.
3. Concatenate all row strings to get the final zigzag output.

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

string convertZigzag(const string &s, int numRows) {
    if (numRows <= 1 || (int)s.size() <= numRows) return s;

    vector<string> rows(min(numRows, int(s.size())));
    int curRow = 0;
    bool goingDown = false;

    for (char c : s) {
        rows[curRow].push_back(c);
        if (curRow == 0 || curRow == numRows - 1)
            goingDown = !goingDown;
        curRow += goingDown ? 1 : -1;
    }

    string result;
    for (auto &row : rows)
        result += row;

    return result;
}

int main() {
    string s = "PAYPALISHIRING";
    int numRows = 3;

    cout << "Input: " << s << ", numRows = " << numRows << '\n';
    cout << "Output: " << convertZigzag(s, numRows) << '\n'; // Expected: PAHNAPLSIIGYIR
    return 0;
}


