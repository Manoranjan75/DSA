# 🔹 Convert Roman Numeral to Integer (C++)

---

## 🧠 Problem Statement

Given a **Roman numeral** string `s`, convert it into its **integer value**.

---

### 🔹 Examples

- "III" → 3
- "LVIII" → 58
- "MCMXCIV" → 1994


---

## 💡 Roman Numeral Basics

| Symbol | Value |
|:-------|:------:|
| I | 1 |
| V | 5 |
| X | 10 |
| L | 50 |
| C | 100 |
| D | 500 |
| M | 1000 |

---

### 📜 Rule

- If a **smaller numeral** appears **before** a larger one → **subtract** it.  
- Otherwise → **add** it.

**Examples:**
Input:  MCMXCIV
Output: 1994

Input:  LVIII
Output: 58

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int romanToInt(string s) {
    unordered_map<char, int> roman = {
        {'I', 1}, {'V', 5}, {'X', 10},
        {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}
    };

    int total = 0;
    for (int i = 0; i < s.size(); i++) {
        if (roman[s[i]] < roman[s[i + 1]])  // subtraction case
            total -= roman[s[i]];
        else
            total += roman[s[i]];
    }
    return total;
}

int main() {
    string s;
    cout << "Enter Roman numeral: ";
    cin >> s;

    cout << "Integer value: " << romanToInt(s) << endl;
    return 0;
}
