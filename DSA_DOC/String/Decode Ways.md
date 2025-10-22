#  Decode Ways (C++)

---

##  Problem Statement

You are given a string containing digits (e.g., `"12"`),  
where each digit or pair of digits represents a letter according to this mapping:

| Letter | Code | Letter | Code |
|---------|------|---------|------|
| A | 1 | N | 14 |
| B | 2 | O | 15 |
| C | 3 | P | 16 |
| D | 4 | Q | 17 |
| E | 5 | R | 18 |
| F | 6 | S | 19 |
| G | 7 | T | 20 |
| H | 8 | U | 21 |
| I | 9 | V | 22 |
| J | 10 | W | 23 |
| K | 11 | X | 24 |
| L | 12 | Y | 25 |
| M | 13 | Z | 26 |

Your task is to determine **how many possible ways** the string can be decoded.

---

##  Examples
- Input: "12"
- Output: 2
- Explanation: "AB" (1,2) or "L" (12)


---

##  Approach — Dynamic Programming (DP)

We use a **DP array** `dp[i]` representing the number of ways to decode the substring up to index `i`.

### Steps:

1. **Base Cases:**
   - `dp[0] = 1` → Empty string has one valid way (do nothing).
   - `dp[1] = 1` → If the first character is not `'0'`.

2. **Transition:**
   - For each position `i` (starting from 2):
     - Extract last **one digit**: `s[i-1]`
       - If it's between `1` and `9`, add `dp[i-1]`.
     - Extract last **two digits**: `s[i-2]s[i-1]`
       - If it's between `10` and `26`, add `dp[i-2]`.

3. **Final Answer:**
   - Return `dp[n]`, where `n` is the length of the string.

---

##  Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int numDecodings(string s) {
    if (s.empty() || s[0] == '0') return 0;

    int n = s.size();
    vector<int> dp(n + 1, 0);
    dp[0] = 1;  // Empty string
    dp[1] = 1;  // First char (not '0')

    for (int i = 2; i <= n; i++) {
        int one = s[i - 1] - '0';             // single digit
        int two = stoi(s.substr(i - 2, 2));   // two digits

        if (one >= 1)
            dp[i] += dp[i - 1];               // valid single-digit
        if (two >= 10 && two <= 26)
            dp[i] += dp[i - 2];               // valid two-digit
    }

    return dp[n];
}

int main() {
    string s;
    cout << "Enter the numeric string: ";
    cin >> s;

    cout << "Number of ways to decode: " << numDecodings(s) << endl;
    return 0;
}


