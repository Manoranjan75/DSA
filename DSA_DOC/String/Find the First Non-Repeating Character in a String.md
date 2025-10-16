#  Find the First Non-Repeating Character in a String (C++)

---

##  Problem Statement

Given a string `s`, find the **first character** that appears **only once** in the string.  
If no such character exists, display a message indicating so.

---

###  Examples
- "swiss" → 'w'
- "aabbcc" → No non-repeating character


---

## ⚙️ Approach

We use a **frequency array** to count how many times each character appears.

### Steps:
1. Create an integer array `freq[256]` to store frequencies of all ASCII characters.
2. Traverse the string once to **count occurrences**.
3. Traverse it again to **find the first character with frequency = 1**.
4. If no such character exists, return `'\0'`.

This ensures we find the **first unique character** efficiently, preserving the order of appearance.

---

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

char firstNonRepeating(string s) {
    vector<int> freq(256, 0); // store frequency of each ASCII character

    for (char c : s)
        freq[c]++;

    for (char c : s)
        if (freq[c] == 1)
            return c; // first non-repeating character

    return '\0'; // none found
}

int main() {
    string s;
    cout << "Enter a string: ";
    cin >> s;

    char result = firstNonRepeating(s);

    if (result != '\0')
        cout << "First non-repeating character: " << result << endl;
    else
        cout << "No non-repeating character found!" << endl;

    return 0;
}

