#  Remove All Duplicate Characters from a String (C++)

---

## Problem Statement

Given a string `s`, remove all **duplicate characters** while preserving the **original order** of appearance.

---

### Examples
- "programming" → "progamin"
- "banana" → "ban"****


---

## ⚙️ Approach

We use an **unordered_set** to keep track of characters that have already appeared.

### Steps:
1. Create an empty string `result` and an unordered_set `seen`.
2. Traverse each character in the input string:
   - If the character **has not** been seen before → append it to `result` and mark it as seen.
   - If it **already exists** in the set → skip it.
3. Return the final `result`.

This ensures:
- Each character appears **only once**.
- The **order** remains the same as in the input.

---

## ✅ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

string removeDuplicates(string s) {
    unordered_set<char> seen;
    string result = "";

    for (char c : s) {
        if (seen.find(c) == seen.end()) {  // if not seen before
            result += c;
            seen.insert(c);
        }
    }
    return result;
}

int main() {
    string s;
    cout << "Enter a string: ";
    cin >> s;

    cout << "After removing duplicates: " << removeDuplicates(s) << endl;
    return 0;
}


